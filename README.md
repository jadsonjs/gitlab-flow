# GitLab Flow

***Jadson Santos - jadsonjs@gmail.com***

***Last updated: 16/05/2021***


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


A very popular flow is the [Github flow](https://guides.github.com/introduction/flow/index.html) The Github flow is a very simple flow, however, it assumes that you can deploy it in production whenever you merge a feature branch into the master. 

**GitLab flow** tries to solve this problem by creating branches that represent the company's internal environments, there are more possibilities for testing and finding errors. Tests are carried out in all environments until production branch is reached.


<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/gitlab_flow.png" width=500 align=center>


GitLab flow has official documentation, but in my opinion, this documentation is just a flow description, it does not show in detail how the flow works, step by step. For this reason, I have created this document. This documentation tries to explain, in my understanding, each step you should execute to follow this flow. For enhancements and hotfix cycles.

### Principles

   - Create a new local branch for the task and periodically **push a branch of the same name on the server**
   - When the task is finished, **request a Merge Request** for the master branch
   - When the submitted changes were reviewed/approved, merge them with the master branch
   - Once in the master, the code must be **integrated into the company's internal environments** branches, until reaching the production branch.
   - When being merged into the master, **delete the branch** where the task was developed leaving the repository more organized.

### Advantages

   - This flow guarantees a clean state in the branches at any point in the project life cycle.
   - It defines how to do Continuous Integration and Continuous Delivery
   - It is very flexible according to the team's decisions
   - It is less complex than GitFlow Workflow

### Disadvantages

   - It is more complex than GitHub Workflow
   - Git's history becomes unreadable due to the various Merge Requests between branches.

### GitLab Flow vs GitHub Flow

The biggest difference between GitLab Flow and GitHub Flow are the branches of the environment in GitLab Flow (for example, pre-production and production)
GitHub flow assumes that if you are on the master you can go to production. GitLab flow allows the code to pass through internal environments before it reaches production.

### GitLab Flow vs GitFlow

GitLab flow is more favorable to the application of Continuous Integration then Gitfow. The division master/develop makes the Continuous Delivery and the Continuous Integration harder with Gitflow. In GitFlow the creation of branches such as hotfix and release can make integration complex.


 ## GitLab Flow in practice  

### Enhancement flow

The flow starts with the **master** branch, the **pre-production** environment branch, and the **production** environment branch. All these branches should be
protected, for developers do not commit directly to them.


<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow1.png" width=600 align=center>

In the same way as in GitHub flow, to start a new development demand, you must create a specific branch for this demand and periodically perform pushes for branch of the same name to the remote repository.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow2.png" width=600 align=center>

Upon finalizing the demand, a *Merge Request* for the master is requested. A code review can be opened in GitLab and a discussion about the change can be started

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow3.png" width=600 align=center>

When approved, the change must be integrated into the master branch.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow4.png" width=600 align=center>

A merge must then be made between the **master** branch and the pre-production environment branch. A pipeline should be executed to build the project and run the automated tests.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow5.png" width=600 align=center>

When passing in the automated tests, a merge must be done for the production branch. A pipeline should be executed again, to run the automated tests one more time and deploy to production.

 A tag must be created to mark a stable version of the system and the feature branch must be removed to make the repository more organized.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow6.png" width=600 align=center>

### Hotfix flow

In the event of an urgent change that cannot wait for the master to be merge in production. It is possible to create a branch to realize the urgent task from the production branch. This would be a flow equivalent to the "hotfix" branch of GitFlow.

Usually, these urgent changes are error corrections. And few commits are made.

Let's start with a repository where there are 2 tasks committed to the master branch, but which have not yet been made available in production.
Suddenly, an error arises to be corrected in production as soon as possible.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow7.png" width=600 align=center>

Create an error correction branch from the production branch.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow8.png" width=600 align=center>

Push the branch to the remote repository.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow9.png" width=600 align=center>

Request a *Merge Request* for the master branch. Usually, as in the enhancement flow.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow10.png" width=600 align=center>

Wait for the *Merge Request* to be approved and the build of the master branch to pass, indicating that there are no errors in your commit.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow11.png" width=600 align=center>

When automatic tests pass in the master branch, due to urgency, you should not wait for the master branch to be merged in other environments branches. Make a *merge / merge request* **from your feature branch** to **all** other branches of internal environments.

As your feature branch is the production branch with your new commit, usually just a unique commit will be merged to the production branch. Make sure to merge these changes to all environments branches. Or the error correction / urgent change can be lost.

Create a tag, to mark a new system version.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow12.png" width=600 align=center>

Only now delete the error correction branch. The enhancement branches remain in the repository and your correction is in all environments of the system.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow13.png" width=600 align=center>

When the rest of the changes are completed, the improvements will be made available in production without erasing the error correction, as it was already integrated into the master branch of the project. 

A version tag with improvements is marked.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow14.png" width=600 align=center>

At the end of the cycle, all changes are published in production. All non-permanent branches are deleted. The flow is finished and a new cycle begins.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow15.png" width=600 align=center>

Alternatively, for urgent tasks, you can use the **cherry-pick** command to get just a specific commit and send it to the other system environments.
So, for example, you can send only one specific commit to production while the others are still waiting for manual tests to finish, in the pre-production branch.

<img src="https://github.com/jadsonjs/gitlab-flow/blob/master/images/flow16.png" width=600 align=center>



An important thing in this flow is that commits should always be integrated from master to production. Never in the opposite way. As said in the original GitLab flow documentation: **"This workflow, where commits only flow downstream, ensures that everything is tested in all environments. "**

Master -> Pre-Production -> Production (OK)

Production -> Pre-production -> Master (ERROR)

Despite the name, the GitLab flow is not a flow to be applied just on gitlab.com. Can be used with any repository the uses Git.

### A word about Squash Commits
It is often a good idea to use [squash commits](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt---squashltcommitgt), in order to maintain a clean and readable Git history. But there are a few points to keep in mind when using GitLab Flow with quashing.

The peculiarity of a squash commit is that a new commit (with a new SHA-1 hash) is created. Thus the git history of the branches would differ when a merge request is squash merged first into the master branch and then into the environment branches. This would make it more difficult to merge between environment branches.

### Enhancement flow
When a new feature is merged into the master branch, you can use squash commits without hesitation. In the best case you should delete the function branch directly after the merge.

But whenever the master branch is merged into an environment branch, you must never use quash commits, as this would result in different git histories for the branches.

### Hotfix flow
When a hotfix is needed, you must be carfully. Never squash merge the remote hotfix branch into several branches, as each squash merge would result into a new commit (with different SHA-1 hashs).

You can either squash merge the hotfix branch into the production branch, then delete the hotfix-branch, and then merge the production branch back into the master branch and the other environment branches.

Or you can squash merge all commits of the hotfix branch ('error_A') into a new hotfix branch ('error_A-final'). This new hotfix branch can then be merged into all environment branches without squashing.
