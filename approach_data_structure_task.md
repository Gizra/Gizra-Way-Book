# How to approach a new task, and its underlying data structure 

When approaching a new task, it may seem overwhelming because you don’t know from where to start.

In this chapter we will present a method that includes a few steps of logical thinking to help you find the starting point. The task is understanding the set of requirements for implementation and it is done by first finding the underlying data structure.

A task is often composed of many small parts. We need to break the "problem" down to atom parts and reveal the entities and the relationships between them. It is ultimately a world of circles, lines, and arrows.

Take a look at the following simple scenario: 


> Authors can write articles.


Let's try to identify the entities and relationships in this scenario. An amazingly quick and simple way to do it is to draw it by hand. Use circles for entities and lines for the relationships between them.

![](111.jpg)

That wasn't so hard, was it? In this case, the entities are `author` and `article`.  The line indicates that they are somehow related.

A relationship defines how entities relate, so we can use arrows to express the reference between the entities. In order to know the direction of the arrow, we should ask two important questions:

**Question 1:** Can the author write more than one article?

Answer: Yes, she can! So, let's represent that in the sketch. It would look like this:

![](2.jpg)

And, if our author is particularly diligent, she can even write a million articles (theoretically of course), so this brings us to the next important question:

**Question 2. The Million Question** Can and should a single `author` entity refer to a million `article` entities?

Answer: No, the answer is definitely not. It would be a bad idea. 

To understand this, we need to talk about the **meaning of reference**. When object A refers to object B it means object A “knows” about object B. This "knowing" becomes part of the information that object A holds.  So for example when we call object A from the database, it might also retrieve the information of all the "B" objects that it refers to. So, if theoretically there can be a million "B" objects, the system would retrieve them all. This is a very heavy task for the system that requires a lot of memory resources. We want to avoid this.

Therefore we don’t want the `author` to refer to a million `articles`. The `article` will refer to (know about and hold the information on), the `author`.

It looks like this:

![](3.jpg)


Now let's add more details to our scenario:


> Author can write articles on various topic(s).


What is this new topic? Simple - It's an entity, represented as a circle.
How does `topic` relate to the other entities?
Articles are written on particular topics, so the `article` and the `topic` have a relationship.

![](4.jpg)

Now, what is the direction of the relationship? That is, what is referring to what? Let's apply our questions to answer this:

Question 1: Can one `topic` be written about in more than one `article`? Yes.

Question 2 (The Million Question): Can and should one single `topic`refer to a million `article`? No, we don't want that.

Now ask the same questions from the other direction:

Question 1: Can one `article` be written in more than one `topic`? Yes, that is the requirement.

Question 2 (The Million Question): Can and should one single `article` refer to a million `topic`?
This is where reality dictates the answer. While in theory an article could reference a million topics, we know that this won't be the case. A typical article (blog post) will probably have a single or few topics. So, it is safe to say, that based on the limitation which is derived from the fact we are building _real_ sites and not answering academic papers, the `article` refers to the `topic`.

![](5a.jpg)


### Advanced requirements

Up until now nothing was too complicated. Even if you are not a web developer, you are probably comfortable with the above logic. You may be tempted to think that the below scenerio will require some deep understanding of computer science. It doesn't!

The above logic can assist us even with the next scenarios:

> We are going to build a premium Website that contains articles. People can sign-up and register to one or more topics of interest. Registering to a topic means that they can read articles that belong to it.

In this scenerio, we can use the general word for the people who use the system - `user`. In the previous scenerio we called the `user` entity by the more specific name `author`but essentially they are the same.

We know that the `user` has a relationship with a `topic` so we draw a line between them. 

Question 1: asked in both directions
Can a `user` register for more than one `topic`?
Can a `topic` be chosen by more than one `user`?

The answer 'yes' to this question (in both directions) is draws like this:
![](6.jpg)


Question 2 (The Million Question): 
Can and should one single `topic` refer to a million `user`?
Can and should one single `user` refer to a million `topic`?

Hmm, seems we have a real problem here! A single `user` cannot reference million `topic`, and vice versa. Is the universe going to collapse into itself?! 

Worry not, because we have an elegant solution for cases like this. We'll simply create a new entity! We will place it in between the other two entities to solve the out-of-control referencing of a million in both directions. We call this "revealing the entity", as sometimes an entity will be hidden in the requirements and not get an explicit name. In our case, giving it a name shouldn't be too hard. We can call it `membership` and it will represent a specific registration (or a membership) of a user to a topic. Now every `user` has only one single `membership` per `topic`.

![](7.jpg)

By having a special entity for capturing the membership, we can actually add more meta-data like the state of the membership (is the user an active member, pending or even blocked)or timestamp (when the `membership` was created) and so on.

Side note: It's worth mentioning that this `membership` entity and its references is the base concept for the Organic Groups module in Drupal.
But we must continue, it seems that our client has more needs for their premium website.

> Registration should expire after a year. The member will get a reminder emails after 3 month, 1 month and 1 day before expiration. If not renewed, the membership should be set to pending.
 
What information do we need in order to send the reminder emails?

We need to know, of course, when the membership began, so we can calculate when 9 months has passed to send the first reminder email. In technical words, the beginning date or any other date that represent that something has occured in the system is called a `timestamp`.

But this information is not enough. Think about a situation where the user decides not to renew his registration. What happened to his membership? Does it go away, get deleted from the system? Well, usually we don’t delete content from the system, but we can mark it as inactive.

So in order to send the user a reminder, we need to know two things:  the membership created date (`timestamp`) and if it is active or not (`status`).

![](9.jpg)

Now we have all the information we need for sending the first reminder email (the one that comes after 9 month), so in order to know to which user we need to send that email, we need to retrieve from the database the right user. 
Let’s describe in words the query for getting the right information from database:


Give me all `membership` that their `status` is **active** and their `timestamp` is **today's date minus 9 month**.


Ok, we almost there, but there is still one more thing - we need to check that we don't send the email more then one time to the same user. Assuming that we have a lots of `membership` in our database, so we need to limit the number of `membership` we get every time we run the query (if the system will bring us all the fit `membership` at ones, it can be run out of memory). So for example we will tell the system to brings us only 100 `membership` at a time, and we will run the query every 5 min. 

How do we make sure that the system won't bring us the same `membership` we already sent email for 5 min ago?

We need to save the information for which `membership` we already sent emails, and check it every time we want to send reminder email.
But where are we going to save this information?
Is it going to be at the `user` entity? Well, remember that `user` can have more than one `membership`, so it will be very complex to put all this data at the `user` entity. Additionally, the email sends based on a membership's timestamp, so it makes more sense that the `membership` will hold the information about the emails who was send. Well, this won't be good enough ether, because we need to send three emails (3 month, 1 month and 1 day before the membership expire), and it's to much data to put at at the `membership` entity.

In that case it will be better to create new entity. Let's call it `email log`.


![](10.jpg)

Now we need to define the relationship. the `email log` has relationship with `membership` (and not with the `user` if you happen to think so) because we already mentioned that an email sent based on a `membership` data (`timestamp` and `status`).
We know `membership` and `email log` have a relationship, but what refers to what (direction of the arrow)?

**Question 1:** can one `membership` has million `email log`? No it can has maximum three `email log` . 

Because the answer is no, we don't need to ask the million question. we can decide that `membership` will refer to `email log`, because when we retrieve `membership` from the database, we want to get also the information about the `email log`.


![](11.jpg)


Finally, let's describe the exact query:


Give me all ```membership``` that their ```status``` is **active**, and their ```timestamp``` is **today's date minus 9 month**, and we didn't sent email yet to the user who created this membership.




**Summary:**

In our developing websites world, we are facing with new tasks on a regular basis. Even a complex task can be simple to approach if we adopt clear principles:
1. Define the entities. No matter how complex the task is, always start from drawing the first circle (entity) and then continue to the next one.
2. Define the relationships between the entities - what refer to what. Use 'The million question' to help you out.
3. Remember you can create additional entity in case we have complex relationships between two entities. 
4. Describe your "asking for data" (i.e. query) in human words, don't jump to use technical words.




