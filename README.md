# Gitlab Flow
This document show the Gitlab flow in practices.


## Official Documentation

- [Introduction to GitLab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)


## Introduction

![git lab flow image](https://github.com/jadsonjs/gitlab-flow/blob/master/images/gitlab_flow.png | width=300 )

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