Working with QA

# Dev-QA interface

---

In Gizra QA is an inherent part of the dev process. An issue goes through the following life cycle:

1. issue development
2. **simple test development**
3. code review
4. CI
5. merge
6. deploy to dev/test
7. **manual QA**
8. deploy to LIVE
9. **additional automation**

In this chapter, we will describe the process that creates and defined steps 2, 7, and 9 above.

**Simple test development:**

Responsibility: the developer who developed the issue

Preparation: not needed

Description: 

After each issue development, and as part of the code that encapsulates the issue, the developer creates at least 1 simple test for the issue. No issue development is considered complete until a test is created for it, and the test code is reviewed in the code review session \(3\).

**Manual QA:**

Responsibility: the manual QA team member.

Preparation: read the original issue and the full discussion there, to be well informed about the requirements of the issue, as well as aware of any pitfalls that might arise due to the implementation. For example, changing the data structure might have implications and might create bugs in other areas of the project.

Description:

Manual QA is actually the last barrier before the product is deployed \(and the re-deployed over and over again\), and before any new feature is introduced to the users.

While the dev team members always try to think outside the box, it is only natural to get immersed in the details of a specific issue, and sometimes lose sight of what might be the affect of the newly introduced changes on the code. Yes, dev team member will write a simple test \(2\). Yes, the issue will go through code review \(3\) and CI \(4\), however none of the above guarantees that 

1. The feature is satisfying all client requirements that were mentioned in the issue
2. No other feature is harmed by the changes introduced 

The above 2 points are the major focus of the Manual QA.





* QA process \(should be a separate article?\)

* Manual tests

* automation



