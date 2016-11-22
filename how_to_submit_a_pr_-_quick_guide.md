# How to submit a PR - Quick guide


## Objective

After reading, you will know how to submit PR for code review.



## Prerequisite

* I Understand the project goal and what is its main purpose.
* I know who are the team lead and project manager.



## The Flow

1. Open your task on Github: Go to `Project` tab, click on `Weekly Workplan`, under your name you will see all your tasks in the project.
2. Read the description and move the issue to `Today in Progress`. See if you understand, write any questions you feel to fully understand.
3. Check the timeboxing and see if it make sense to you. If it doesn’t, communicate that to your team lead.
4. Write user stories (in [Behat format](http://docs.behat.org/en/v2.5/guides/1.gherkin.html)), to be used for the QA team and automated test.
5. If the issue include writing a new feature, write the outline of the solution. If you feel unsure, tag your team lead.
6. Make sure your master branch is updated.
7. Create a new branch named after the issue number with a tiny description. (ie. 450-fixing-feature).
8. Create PR with WIP prefix in the title, assign it to yourself.
9. Start coding, push code regularly to allow code review during your work.
10. When work is done and ready for review, push the final code.
11. Go over the user stories and check your work at least once for each case. If this is a bug make sure to include in your testings the **exact** scenario of the bug, and to add this scenario to the user stories.
12. Code review yourself first, then make sure travis return green (both with Coder and Tests).
13. Add a screenshot.
14. When all done, remove WIP from PR title, assign to Team Lead developer for review, and add relevant label.

Read [Pull Requests](https://www.thegizraway.com/pull_requests.html) for more information.


## Coding standard 
 
Make sure you know the coding standard required for the language, coder should run on your files to validate this. 


## Issue tracking and Bugs

Use Github issue tracking to document your work and progress when necessary, especially when working on bugs. This will allow other developers to help, and stakeholders to track your progress.


## GH Issue Flow


Typically an issue is opened by the account manager, or by the QA team/ Customer, the basic rule of thumb is that an issue  is closed by the person who opened it.

Account managers or Team leads are responsible to assign issues to other team members.


## Focus and Follow Up issues

During your work try to stay on track, for bugs if you feel a quick solution can be thrown before dipping into proper solution, please consult with your team lead.
Any indirect issue you find during your work should be translated to a new follow up issue, and documented in your GH issue.  
make sure you don't have more than 2 or 3 missions in progress. stay focused.


## Automated Test

Check if a test should written with your team lead or write one if you have extra time out of your timebox.


## How deal with a problem

Read [How to solve a problem](https://www.thegizraway.com/how_to_solve_a_problem.html).



## Checklist


[ ] - Pull latest code from the master branch.  
[ ] - Reinstall project and test your feature/check the bug.  
[ ] - Run coder.  
[ ] - Code review yourself.  
[ ] - Comment on all functions and comment complicated part of your code, be generous.  
[ ] - Security check your code.  
[ ] - Add a screenshot.
[ ] - Test your code.  
[ ] - Add a wiki entry when needed.  
[ ] - Add a user story.  
