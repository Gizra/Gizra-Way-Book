# Approaching a Task - determining a website's technical structure. 

When you need to deal with new task, sometimes things seem confusing and even a simple task may be overwhelming because you don’t know from where to start. Well, no need to reinvent the wheel, once you adopt a clear approach to a problem, with defined rules, ever the most complex task becomes approachable and less threatening.

In this post we present a method that includes a few steps of logical thinking to help you find the starting point from which to approach a task. A task being the determination of a website's technical structure.

First of all, we can think about a mission as a story plot with characters. A well written and understood story plot includes clearly defined relationships between the characters.

In our technical world, characters are called entities, and the first step to understanding the story, our new mission, is to be able to recognize the entities and the relationships between them.

Take a look at the following simple story: 


> An author writes articles.


Let's try to identify the entities and relationships in this story. The best way to do it - is to draw it! Use circles for entities and lines for relationships.

![](111.jpg)

In this case, the entities are `author` and `article`.  The line indicates that they are related.

A relationship defines how entities are related to one another, so we can use arrows to express the reference between the entities. In order to know the direction of the arrow, we should ask two important questions:

**Question 1:** Can the author write more than one article?

Answer: Yes, she can! So, let's represent that in the sketch. It would look like this:

![](2.jpg)

And, if our author is particularly diligent, she can even write a million articles (theoretically of course), so this brings us to the next important question we call:

**Question 2. The Million Question** Can the entity `author` refer to a million `article` entities?

Answer: No, the answer is definitely not. 

To understand that, we need to understand the **meaning of reference**. When object A refers to object B it means object A “knows” about object B, and this “knowing” becomes part of the information that object A holds.  So when we call object A from the database, it will also retrieve the information of all the “B” objects that it refers to. So, if theoretically there can be a million “B” objects, the system would retrieve them all. This is a very heavy task for the system that requires a lot of memory resources. We want to avoid this.

So because we don’t want the `author` to refer to a million `articles`, the `article` will refer to (know about and hold the information on), the `author`.
It looks like this:

![](3.jpg)


Now let's add more details to our story:


> Author writes articles on various topics.


Now we have another entity called `topic`. How does `topic` relate to the other entities?
Articles are written on particular topics, so the `article` and the `topic` have a relationship.

![](4.jpg)


What refers to what (direction of the arrow)? Let's use our questions:

Question 1: Can one `topic` be written about in more than one `article`? Yes.

Question 2: (The Million Question) Can one `topic`refer to a million `article`? No, we don't want that.

Now use the questions the other way around:

Question 1: Can one `article` be written on more than one `topic`? Theoretically yes, but to keep things simple let's assume that every article belongs only to one topic. In that case the answer to this question is no.

Question 2: We don't need to ask the Million Question since the answer to the first Question is 'no'.

Now we know that the Article refers to the topic. Here it is represented by the arrows:
![](5a.jpg)


Our story continues... 


> We are going to build a Premium Website that contains articles. People can sign-up and register to one or more topics that interest them. Registering to a topic means that they can read articles that belong to it.


Now we have new entity: people.  Let's call it `user`.

Question 1: Does a `user` have a relationship with a `topic`?
Can a `user` register for more than one `topic`?
Can `topic` be chosen by more than one `user`?

Well, user can register to many topics and many users can register to the same topic, so we will get something like this:

![](6.jpg)


Question 2: (The million question) In this case, it gets a bit complicated, huh?! It can be a million users and a million topics... how can we solve it? 
We can add another entity, called `membership`. It will represent a specific register of user to a topic. Now every user has only one `membership` per topic.

![](7.jpg)

In this case `membership` refer to `topic` (because we don’t want `topic` refer to million `membership`). `membership` also refer to `user` (because we don’t want `user` refer to million `membership`). It looks like this:

![](88.jpg)



Continue with our story - 


> Registration expired after a year. The user will get a reminder emails - 3 month, 1 month and 1 day before expired, so he can renew his registration.
 

What information do we need in order to send the reminder emails?

We need to know of course when the membership began, then we can calculate when 9 months has passed and send the first reminder email. In technical words, the beginning date (or any other date represent something occurs in the system), calls `timestamp`.

But this information is not enough. Think about situation user decide not to renew his registration, what happened to his membership? Is it going away, delete from the system? Well, usually we don’t delete content from the system, but we can mark it as inactive.

So in order to send the user reminder, we need to know two things:  the membership created date (i.e `timestamp`) and if it is active or not (i.e `status`).

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
1. Define the characters (entities) in the plot.
2. Define the relationships between the entities - who refer to whom. Use 'The million question' to help you out.
3. Describe your "asking for data" (i.e. query) in human words, don't jump to use technical words.




