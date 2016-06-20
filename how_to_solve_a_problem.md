# How to Solve a Problem

Mastering problem solving will get you very far. There are some techniques to do it, and it's important
to be aware of the fact your day is mostly composed of problems that need to be solved.

A dev who encounters a nasty bug; An account manager working on a price estimation; A sales person trying to reach more leads. These are all big problems, which probably have solutions.

As we will refer to "problem" as "bug" this chapter might seem as relevant only for developer. However the mind set applies to all the roles in the company.

## Finding the cause

Understanding the cause of the bug is the first step and the most important one, in the task of solving. Only in very rare cases where a serious bug happens in production and we want to first patch the bug with some quick fix, we will start by "solving" the problem. But we'll always circle back at finding the cause.

It's better to reflect on the term "the cause". Are you sure the cause you are seeing is the "root cause"?
Systems are always convoluted, and miss identification of the real cause, will cause the bug to appear in different places.

Assumptions are good but need to be taken with a pinch of salt. You shouldn't dive in too deeply just based on your assumption, without verifying it. For example, don't waste time on debugging a certain module before you have asserted that it's indeed the one to blame.

The first step for diving into a system for finding a bug is not using a scalpel, but rather a D9. This means that the first steps don't require slow and tedious debugging of every line of code, but rather big and radical changes. Examples:

Problem: You think a bug is a result of some module. You are not sure exactly which line
Solution: Completely delete the file

Problem: You are not sure if a wrong output of the screen is the result of wrong code in the theme
Solution: Change the theme to under one, thus completely remove all the theme's code from the equation.

Problem: Your new shiny code doesn't work
Solution: Check if it is even invoked. Again, no need to have very delicate debugging. Instead trace the places the code is being called and figure out if is indeed called

Problem: Something that used to work stopped working
Solution: You are in luck, because you can try and find the working instance (e.g. go back in Git's history). If you are able to find a working example, the next step is to pin point the exact time in history (i.e. the git commit) that broke things.

As you can see the gist of the examples is to work out as quickly as possible in getting into right area. From there starting pin pointing the problem.

The next question you need to ask yourself, is did it change anything?
If yes, you know you are in the right area, keep zooming in.
If not, you know you are barking at the wrong tree. Use your D9 to squash other parts.

![Caterpillar D9](images/solving_problem/image1.jpg)

### Time boxing

Like any task you must be disciplined and time box your efforts. Sometimes to _root cause_ can be buried
very deep inside a legacy very complex system. For example, trying to find the root cause of Drupal's from API
can be very challenging. There are times it's needed, but there are cases a work around would be easier.

The way to decide when to move to a work around solution, is the time boxing. If you are about to exceed the time allocated, it might be time to also investigate what are the work around options.

In any case, as always, be sure to reach out to other team members to see if they have a similar experience or a different suggestion.

To emphasize, a work around is a valid solution, but it's kept as the last one. Having a work around is adding a lot of technical debt to the system. Meaning, you have solved a problem, but most likely created new future ones, so be careful with this solution.

## Taking responsibility

## Escalation
