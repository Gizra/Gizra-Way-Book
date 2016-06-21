 # How to Solve a Problem

Mastering problem solving will get you far. There are some techniques to accomplish this, and it's important to be aware of the fact that your day is mostly composed of problems that need to be solved.

A dev who encounters a nasty bug; an account manager working on a price estimation; a salesperson trying to reach more leads. These are all big problems, which probably have solutions.

As we will refer to "problem" often as a "bug" this chapter may seem only relevant for a developer. However, the methods and mindset applies to all the roles in the company.

## Finding the cause

Understanding the cause of the bug is the first step and the most important one. Only in very rare cases where a serious bug happens in production, would we want to first patch the bug with a quick fix, working around the problem, before circling back to find the cause.

Let's take a moment to reflect on the term "the cause." Are you sure the cause you have identified is the "root cause"?
Systems are convoluted, and miss-identification of the real cause, will result with the bug simply appearing at different places.

Assumptions are good but need to be taken with a grain of salt. You shouldn't dive in too deeply based on an assumption without verifying every step. For example, don't waste time on debugging line by line a certain module before you have asserted that it's indeed the one to blame.

The first step for diving into a bug is not using a scalpel, but rather a D9 tractor. This means that the first steps will not require slow and tedious examination of a lot of code, but rather big and radical changes. Examples: 

| Problem | Solution |
| -- | -- |
| You think a bug is a result of some module. You are not sure exactly which line. | Completely delete the file, and confirm there was indeed a change. |
| You are not sure if a wrong output of the screen is the result of wrong code in the theme. |  Change the theme to another one, thus completely removing the theme from the equation.|
| Your new shiny code doesn't work. |  Check if it is even invoked. Again, no need to have a very delicate debugging session. Instead, trace the places the code is being called and figure out if it is called as you assume. |
| Something that used to work stopped working. | You are in luck, because you can try and find the working instance (e.g. go back in Git's history). If you are able to find a working example, the next step is to pinpoint the exact time in history (i.e. the git commit) that broke things, and then you'll have a smaller diff to investigate. |

After each of these above solutions, we ask ourselves, did it change anything?
If yes, we know we are in the right area, and we keep zooming in.
If not, we know we were barking up the wrong tree. We keep using our D9 to go over other parts of the code until we see a change.

The gist of the above examples is to figure out as quickly as possible the right area of the bug. From there start pin pointing the bug's cause - there is always *one specific line* that causes the havoc.

![Caterpillar D9](images/solving_problem/image1.jpg)

*Caption: D9 going over your project looking for the right place to dig*

### Time boxing

Like any task you must be disciplined and time box your efforts. Sometimes the _root cause_ can be buried very deep inside a legacy or a complex system. For example, trying to find the root cause in Drupal's API can be very challenging. There are times it's needed, but there are cases a work around would be easier.

The way to decide when to move and develop a work around solution, is with time boxing. If you are about to exceed the time allocated, it may be time to also investigate what are the work around options.

In any case, as always, be sure to reach out to other team members to see if they had a similar experience or a good suggestion.

To emphasize, a work around is a valid solution, but it's kept as a last resort. Having a workaround in place often adds a technical debt to the system. Meaning, you have solved a problem, but most likely created new future ones, so be careful with this solution.

## Taking responsibility

Digging into a problem might reveal unexpected stuff, maybe a bug lurking in the shadows.
Don't be distracted by it, as our brain can't process two problems at once, however don't disregard it either. You are expected to open an issue in GitHub, for you or others to address later on.

The term "taking responsibility" refers to owning the code or a piece of work, even if it was authored by others. Nothing's carved in stone, and past developers have not necessarily been smarter than you.

A system is a living thing, that changes over time. You don't need to work around other's code, you can go ahead and fix the problem. A classic example is CSS code, which becomes bloated very quickly. Don't keep adding new classes, if with a slight more effort you can change existing classes or even completely remove them, thus reducing the CSS complexity, then do it!

## Escalation

You are not alone in the never-ending battle of bugs and problems. And most importantly, there is always a client that needs to be updated.

In terms of priority, a bug or some service interruption in a production site needs to be addressed quickly. It does not necessarily mean that a fix can be deployed quickly, but rather communicating with the client and updating them about the resolution and expected time is crucial.

Escalation should happen every time you are about to hit the limit of the time boxed task. If you see you won't be able to accomplish it on time, go ahead and reach out to the team lead, the project owner or even the management in severe cases, so they are aware of the situation and can act accordingly.

Here's a real case we had in the past:

In the production site of a client some emails stopped being sent. That is, some emails were sent, while  others not.

The lead developer started doing some debugging and sent questions to the client, suspecting that they had done some configuration changes.
The client confirmed no config change had been done from their side. It was communicated via the GitHub's issue queue.

The developer re-started efforts to find the cause but did not communicate this to the client. From the client's perspective, not only did their site not work correctly, but they were under the impression that their issue was not being addressed. 

The developer was also responsible for another project, so the issue did not get the full attention it deserved.
A few days later and after the client's CEO called to confirm someone was working on it, the developer gave it some attention. However, again did not send any updates to the client.
After 10 days of what we can imagine a very unhappy client, and on the last day of the work week, the issue was finally properly escalated by the developer.

The escalation was simple, an email to the lead developers stating that the client has a problem for the last 10 days and that they are starting to become impatient.

Two hours later the lead developers found the cause, and the issue was solved in the production site.

---

Let us analyze the above incident. The fact that it should have been escalated sooner, based on the above time boxing guidelines, is probably trivial by now, but there is another point to be made. Let's assume it was a serious bug that required re-writing a substantial chunk of the system. If the client is kept in the dark, they will assume that the issue will be resolved at any moment. However if we  explain to them the problem, and set their expectation to 10-12 days, then they would not be disappointed every single day that passed.

That is one of the big takeaways from this case. The 10 days to find a solution is of course detrimental, especially given the fact that we were able to solve it within 2 hours once more experienced developers stepped in. But what is troubling, is that the client was not aware of the time table, and our efforts were not communicated. So from their perspective, as long as they did not hear from us and the problem was not yet solved, they could only assumed we were not working on it. 

Notice for example that when a lead developer stepped in, four different updates in the issue queue were entered in the span of two hours. Even though it's very technical talk, it provides internally some context, and to the client it shows someone is on it.

![Constantly updating all the stakeholders](images/solving_problem/image2.jpg)

The ramifications of this case is an un-happy client, that will probably not be as patient the next time a system bug presents itself. This is a critical pitfall to avoid. 
It doesn't mean that from now on, every single issue should be pushed up to the management or lead developers. Use time boxing as an indication to when to escalate. The lesson learned here is that we must always remember there is a client with high expectations and we must communicate and manage their expectations, especially during the sensitive period of a system bug. We are doing our best to deliver and they need to know about it.  

**Note:**  It's worth mentioning here that making a mistake is fine. As seen above, a mistake has spurred this case study for all of us to learn from. However, making the same mistake twice is sloppy, and we strive to avoid this.