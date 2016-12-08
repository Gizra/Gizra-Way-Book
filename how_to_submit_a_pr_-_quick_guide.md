# How to submit a Pull Request - Quick guide


## Goal

After reading, you will know how to submit Pull Request (PR) for code review.

## Prerequisite

* I Understand the project goal and what is its main purpose.
* I know who is the team lead and account manager.

## The Flow 

### Flow outline:

1. **Prepare your tasks for the week**
2. **Write some awesome code** that solves your issue.
1. **Test your work and submit for review**

### Flow in detail:

####1. Prepare your tasks for the week
**Note:** *this part should be performed for all your weekly tasks in the first day of the week - this will allow AMs and TLs to review the user stories and proposed technical solutions.*


1. **Open your task** on Github: Go to `Project` tab, click on `Weekly Workplan`, under your name you will see all your tasks in the project and their priority (top one is no. 1 and so forth).
2. Read the description, **Check if you understand the issue**, and if you don't, this is the time to  write any questions. *This is important. Keep asking questions until you understand!*
3. **Check the timeboxing** and see if it makes sense to you. If it doesn’t, communicate that to your team lead. *This will help identify early on any issues with the timebox, how well the task was explained, and if you really understand the task. Giving this thought can save you a lot confusion and frustration later on.  *
4. **Write user stories** (in [Behat format](http://docs.behat.org/en/v2.5/guides/1.gherkin.html)), to be used for the QA team and automated tests.
5. If the issue include writing a new feature, write the **outline of the solution** titled ##"Solution Outline" in the comment. If you feel unsure, tag your team lead.

####2. Write some awesome code

6. On Github: under `Project` tab, move the task to `In progress` column.
7. Make sure your **master branch is updated**.
7. **Create a new branch** named after the issue number with a tiny description. (ie. 450-fixing-feature).
8. **Create PR **with WIP prefix in the title, assign it to yourself.
9. Start coding, **push code regularly** to allow code review during your work.
10. When your work is done and ready for review, **push the final code**.

####3. Test your work and submit for review
11. Go over the user stories and **check your work** at least once for each case. If this is a bug make sure to include in your testings the ***exact*** scenario of the bug, and to add this scenario to the user stories.
12. **Code review yourself** first, then make sure travis returns green (both with Coder and Tests).
13. Add a **screenshot**.
14. **When all done** 
  15. remove the WIP from the PR title 
  16. assign it to the Team Lead developer for review
  17. add relevant label.

Read [Pull Requests](https://www.thegizraway.com/pull_requests.html) for more information.

## Coding standard 
 
Make sure you know the coding standard required for the language - the coder should run on your files to confirm this.

* [How to setup coding standard in PHPStorm](https://www.jetbrains.com/help/phpstorm/2016.2/configuring-code-style.html#d1056806e40).
* [Drupal coding standard](https://www.drupal.org/docs/develop/standards).

## Issue tracking and Bugs

Use Github issue tracking to document your work and progress when necessary, especially when working on bugs. This will allow other developers to help, and stakeholders to track your progress.


## Github Issue Flow


Typically an issue is opened by the account manager, or by the QA team/customer, the basic rule of thumb is that an issue is closed by the person who opened it. 
This mean you can close issues opened by you when they are done and deployed after validation, and other issue should be assign to the account manager.

Account managers or Team leads are responsible to assign issues to the team members.

## Focus and Follow Up issues

During your work try to stay on track, for bugs if you feel a quick solution can be thrown before dipping into a proper solution, please consult with your team lead.
Any indirect issue you find during your work should be translated to a new follow up issue, and documented in your GH issue. Make sure you don't have more than 2 or 3 missions in progress. Stay focused.

## Automated Tests

Check with your Team Lead if a test should written or write one if you have extra time out of your timebox.

## How deal with a problem
Read [How to solve a problem](https://www.thegizraway.com/how_to_solve_a_problem.html).


## Checklist
When a PR is created, this checklist will automatically be in the first comment. **Before you submit the PR**, please make sure that you did all the following things.

[ ] - Merge latest code from the master branch.    
[ ] - Code review yourself.  
[ ] - Comment on all functions and comment complicated part of your code, be generous.  
[ ] - Security check your code.  
[ ] - Add a screen-shot.  
[ ] - Test your code, using the user stories, Add screenshot to the user story results.   
[ ] - Add a wiki entry when needed, or release protocols.  
[ ] - Assign for review.