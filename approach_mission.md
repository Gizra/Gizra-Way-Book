# Approach mission

As a newbie a lot of things seems very confusing and sometimes even a simple task may appear threatening because you don’t know from where to start. Well, no need to reinvent the wheel, once you adopt an approach how to think about a problem, according to clear rules, everything starts to become clear and seem less threatening.

In this post I will try to present method includes a few steps of logical thinking, to help you find the [קצה חוט] from which to start dealing with the mission.

First of all, we can think about mission as a story with a plot and characters. 
What makes a story to be a well written story? The characters and their relationships must define clearly, so we can better understand the plot.

In our technical world we call characters as entities, and our first steps when we deal with new mission, is to be able to recognize the entities in the story and the relationships between them.

Let's take a look of a simple story: 

Author writes articles.

Yes, it’s a story with only one line, but it’s a story. Let's try to recognize the entities and the relationships in this story. the best way to do it is to draw it! We can use circle as an entity and line as a relationship.











A relationship defines how entities are related to one another, so we better use arrow line to express the reference between the entities. In order to know the direction of the arrow, we should ask two important questions:
1. Is the author can write more than one article?
Yes, he can! So it will look like this:

And if our author is particularly diligent, he can write even a million articles (theoretically of course…), so this will bring us to the second important question, we call it “the million question”: 
2. Is the entity “author” can refer to million entities “article”?
No, the answer is definitely not. To understand that, we need to understand the meaning of reference. When object A refer to object B it means object A “knows” about object B, and this “knowing” became part of the information that object A holds.  So when we call object A from the Database, it will brings us also the informations of all the “B”s objects that it refer to. So if there are milion “B”s objects, the systems brings them all. This is a very heavy task for the system to deal with and needs a lot of memory resources … We want to make it easier for the system and not make it difficult for her. 

So because we don’t want “author” refer to million entities “article”, the “article” is refer to “author”. 
It will look like this:













Now let’s add more details to our story:

Author writes articles in various topics.

Now we have another entity “topic”. How does “topic” relate to the others entities?
Article written on a particular topic, then the ״article״ and the “topic” have a relationship.




And who refer to whom? (what is the arrow direction?)
Let’s ask the “million question” - 
Is one topic can has more than one article? Yes.
Is one article can written on more than one topic? Theoretically yes, but for the practice we decide that every article belongs only to one topic, so the answer to this question is No.








Our story continue - 

We going to build a Premium Website, contains articles. People can signup and register to one or more topic that interest them. While they register to a topic, they can read articles belong to it.

Now we have new entity: People.  Let's call it “User”.

Is “user” has relationship with “topic”?

Well, user can register to many topics and many users can register to the same topic, so we will get something like this:






Try to answer the “million question” for this case… a bit complicated, huh?! It can be a million users and a million topics...
So, to make it simple, we can add more entity - let’s call it “Membership”, and it will represent a specific register of user to a topic.



In that case “Membership” refer to “Topic” (because we don’t want “Topic” refer to million “Membership”) and ““Membership” also refer to “User” (because we don’t want “User” refer to million “Membership”). It looks like this:

Let us continue with our story - 

Registration expired after a year. The user will get a reminder emails - 3 month, 1 month and 1 day before expired, so he can renew his registration. 

What information do we need in order to send the reminder emails?
We need to know of course when the membership began, then we can calculate if 9 months has passed and it is time to send the first reminder email. In technical words, the beginning date (or any other date represent something occurs in the system), calls “time stamp”.

But this information is not enough. Think about situation user decide not to renew his registration, what happened to his membership? Is it going away, delete from the system? Well, usually we don’t delete entities from the system, but we can mark them as inactive.
So in order to send the user reminder, we need to know two things:  the membership’s time stamp and if it is active or not.

[drawing with “membership” and “time stamp”, “status=active/inactive”]

Ok, so now we have all the information we need for sending the first reminder email (the one that comes after 9 month), so in order to know to which user we need to send that email, we need to retrieve from the database the right user. 
Let’s describe in words the query for getting the right information from database:

Give me all “membership” that their “status” is *active* and their “time stamp” is *today's date minus 9 month*

Ok, we almost there, but there is still one more thing - we need to check that we don't send the email more then one time to the same user. Assuming that we have a lots of "membership" in our database, so we need to limit the number of "membership" we get every time we run the query (if the system will bring us all the fit "membership" at ones, it can be run out of memory). So we will tell the system to brings us only 100 "membership" at a time, and we will run the query every 5 min. 
How we make sure that the system won't bring us the same "membership" we already sent email for them 5 min ago?





