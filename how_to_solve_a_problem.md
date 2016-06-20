# How to Solve a Problem

Mastering problem solving will get you very far. There are some techniques to do it, and it's important
to be aware of the fact your day is mostly composed of problems that need to be solved.

A dev who encounters a nasty bug; An account manager working on a price estimation; A sales person trying to reach more leads. These are all big problems, which probably have solutions.

As we will refer to "problem" as "bug" this chapter might seem as relevant only for developer. However the mind set applies to all the roles in the company.

## Finding the cause

Understanding the cause of the bug is the first step and the most important one, in the task of solving. Only in very rare cases where a serious bug happens in production and we want to first patch the bug with some quick fix, we will start by "solving" the problem. But we'll always circle back at finding the cause.

It's better to reflect on the term "the cause". Are you sure the cause you are seeing is the "root cause"?
Systems are always convoluted, and miss identification of the real cause, will cause the bug to appear in different places.

The first step for diving into a system for finding a bug is not using a scalpel, but rather a D9. This means that the first steps don't require slow and tedious debugging of every line of code, but rather big and radical changes. Examples:

Problem: You think a bug is a result of some module. You are not sure exactly which line
Solution: Completely delete the file


Problem: You are not sure if a wrong output of the screen is the result of wrong code in the theme
Solution: Change the theme to under one, thus completely remove all the theme's code from the equation.

The next question you need to ask yourself, is did it change anything?
If yes, you know you are in the right file. If not, you know you are barking at the wrong tree.

![Caterpillar D9](images/solving_problem/image.jpg)

## Taking responsibility

## Escalation
