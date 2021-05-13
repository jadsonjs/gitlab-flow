# Gitlab Flow


## Official Documentation

- [Introduction to GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)


## Introduction

Git allows you to create several development flows that meet the dynamics of your company.

You can have an enhancement branch, a maintenance branch, a branch that freezes the code to be approved before going into production, while new tasks for the next release can already be done, etc ...

When working as a team, it is important to have a well-defined git flow, to not generate a complex and inefficient flow.

You need to be sure that the team is in agreement on how the flow will be applied.

There are several cataloged workflows. There is no the best git flow, there is the one that best suits the reality of your team.

What can be considered a successful workflow?
   - Does the workflow adapt to the size of the team?
   - Is it easy to undo mistakes with this workflow?
   - Does this workflow impose any unnecessary new overhead on the team?


A very popular flow is the [Github flow](https://guides.github.com/introduction/flow/index.html) The Github flow is a very simple flow, however it assumes that you can deploy it in production whenever you merge a feature branch into the master. 

**Gitlab flow tries** try to solve this problem by creating branches that represent the company's internal environments, there are more possibilities for testing and finding errors. Tests are carried out in all environments until production branch is reached.


<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/gitlab_flow.png" width=500 align=center>


Gitlab flow has official documentation, but in my opinion, this documentation is just a flow description, it does not show in detail how the flow should works. For this reason, I have created this document. This documentation tries to explain each step you should execute to follow this flow. For enhancements and hotfix cycles.

### Principles

   - Create a new local branch for the task and periodically **push a branch of the same name on the server**
   - When the task is finished, **request a Merge Request** for the master branch
   - When the submited changes were reviews / approves, merge they with the master branch
   - Once in the master, the code must be **integrated into company's internal environments** branches, until reaching the production branch.
   - When being merged into the master, **delete the branch** where the task was developed leaving the repository more organized.

### Advantages

   - This flow guarantees a clean state in the branches at any point in the project life cycle.
   - It defines how to do Continuous Integration and Continuous Delivery
   - It is very flexible according to the team's decisions
   - It is less complex than GitFlow Workflow

### Disadvantages

   - It is more complex than GitHub Workflow
   - Git's history becomes unreadable due to the various Merge Requests between branches.


 ## Gitlab Flow in practice  