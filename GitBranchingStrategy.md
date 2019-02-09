# Git Branching Strategy

## Contents
* [Overview](GitBranchingStrategy.md#overview)
* [Git repository structure](GitBranchingStrategy.md#git-repository-structure)
* [The main branch types](GitBranchingStrategy.md#the-main-branch-types) 
* [The master branch](GitBranchingStrategy.md#the-master-branch)
* [The developement branch](GitBranchingStrategy.md#the-development-branch)
* [Feature branches](GitBranchingStrategy.md#feature-branches)
* [Experimental branches](GitBranchingStrategy.md#experimental-branches)
* [Release branches](GitBranchingStrategy.md#release-branches)
* [Bugfix branches](GitBranchingStrategy.md#bugfix-branches)
* [Hotfix branches](GitBranchingStrategy.md#hotfix-branches)
* [Naming Conventions for branching](GitBranchingStrategy.md#naming-conventions-for-branching)
* [When to branch from Development](GitBranchingStrategy.md#when-to-branch-from-development)
* [Process for merging a feature branch back to master](GitBranchingStrategy.md#process-for-merging-a-feature-branch-back-to-master)
* [Deleting a branch](GitBranchingStrategy.md#deleting-a-branch)
* [Commits message guidelines](GitBranchingStrategy.md#commits-message-guidelines)
* [Code Freeze and Release Process](GitBranchingStrategy.md#code-freeze-and-release-process)

## Overview 

This document describes the workflow and best practices for working in a collaborative development environment with Git Version Control. It is somewhat comprehensive Git Flow Process that I've (with some variations) used in development teams in the past - Some of them might make sense or be an overkill depending on the team dynamics/size/project etc. But it'd be still nice to go over this and adopt things that are relevant to our team here. 


## Git repository structure 

### The main branch types 

There are a few different branch types that all the branches go into. Each of these branches have a specific purpose and are bound to strict rules as to which branches may be their originating branch and which branches must be their merge targets. By no means are these branches “special” from a technical perspective. The branch types are categorized by how we use them. 

#### The master branch 

- The main stable branch - always reflects a production-ready state. 
- Stable - all features are working, unit, functional and integration test are passing 
-  No direct commits are allowed directly to master branch 
- Master branch is tagged 

#### The development branch 

- Branched off from master branch 
- The main working development branch which reflects a state with the latest delivered development changes for the next release. 
- Release branch are made from here 
- QA picks up the released artifacts of this branch from Jenkins for validating and signing off on bug fixes, reporting new issues.

#### Feature branches 

- Branched off from ‘Development’ branch 
- Create PR to merge back to Development branch - wait for at least two approvals
- Short-lived 
- Developers should use feature branches to develop new features, sub-features or improvements without affecting the stability of the development branch. 
- Feature branches should be kept regularly in sync with the development branch. This means merging Development branch into the feature branch regularly.

#### Experimental branches 

- Branched off from Development branch 
- Developers should use Experimental branches, if there is no corresponding tasks created in JIRA. This branch is for experimenting/testing changes to already existing feature in development or new feature 
- Please Create JIRA tickets if it's turning to be new feature/improvement to already existing feature and create appropriate branches for the same
- Experimental branches are not meant to be merged back to Development 

#### Release branches 

- Branched off from Development branch 
- Shields the code base from all but critical changes and fixes 
- All internal releases/public releases are made from this branch. For Example: Say we create a release branch 1.5.0 from Development 
We make internal release from this branch. If we find critical bugs in 1.5.0, we branch off to release/1.5.1 from release/1.5.0 and make the fix. Release 1.5.1 is merged back to Development 
- Is merged back into Development regularly to make fixes available on them. 
- Code commits to this branch follow code freeze process 
- Production release is merged back to master and tagged with the corresponding release version 

#### Bugfix branches 

- Similar to feature branch, short-lived 
- Branched off from Development branch 
- Merged back into Development branch 
- Developers should create bugfix branches to address bugs and issues reported in JIRA, without affecting the stability of the development branch 
- Should be kept in sync with Development branch. 

#### Hotfix branches 
- Branched off of release branch meant for a critical fix that need to go into the release 
- Merged back to the specific release branch 
- Hotfix branch must be closed as soon as they are merged to the specific release. 
Naming Conventions for branching 
- Feature branches: feature/WHAR-XXX-description 
- Bugfix branches: bug/WHAR-XXX-description 
- Release branches: release/ ○ E.g release/1.0.1 
When to branch from Development 
- When your changes could affect the stability of other feature branches 
- When you will need multiple commits to complete your work (i.e. don’t add your feature improvement or bugfix onto development, until it’s done) 
- When working on prototypes or experimenting with something, that you do not plan to merge onto master 

You should only develop directly on the development branch when you are making a very low risk change that is self-contained in one commit. We do not need to be too formal about this while we are not in code freeze towards a public release, so every developer can use their judgement - but when in doubt, branch. 
Process for merging a feature branch back to master 

- First sync the feature branch to the tip of the development, by merging development into your feature branch. 
-  Do a sanity check locally, check if they build well, passes all unit and integration tests 
-  Setup code review 
-  Once code review passes, merge the feature branch into development. 

### Deleting a branch 

- Once a feature branch is integrated into development, and you do not plan any more work on it, you should delete both your local tracking branch for it, and delete the remote branch. 
- First notify all the team members that you will delete the branch, to make sure no one is working on this branch 

### Commits message guidelines 

- Try to make each commit a logically separate changeset 
- Include the ticket number that motivated your change in the commit message 
- E.g. “Fixing trackable object prefab - SSU-212” 

### Code Freeze and Release Process 

Towards the final stage of a release, we enter code freeze mode: 
- A release branch is created by someone in the team who volunteers to own the release process 
- Only critical bugs are addressed 
- Any code change is staged first, subjected to code review 
- Upon successful code review, the person in charge of release is notified to merge the change onto the release branch 
- As of now, all releases are named based on the most recent annotated tag. So at the time of the release, the person in charge will run the shell script to automatically tag the branch, and update the version text file.
