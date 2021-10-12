# Git

## Introduction

**Version Control System: **A version control system (VCS) tracks the history of changes as people and teams collaborate on projects together.

**Git: **Git is a Distributed Version Control System (DVCS) used for open source and commercial software development. DVCS allow full access to every file, branch, and iteration of a project, and allows every user access to a full and self-contained history of all changes.

### Why Git?

Git is used by more than 70% of developers for both open source and commercial software development.

Benefits of Git include:

* Git lets developers see the entire timeline of their changes, decisions, and progression of any project in one place. From the moment they access the history of a project, the developer has all the context they need to understand it and start contributing
* Developers work in every time zone. With a DVCS like Git, collaboration can happen any time while maintaining source code integrity. Using branches, developers can safely propose changes to production code
* Businesses using Got can break down communication barriers between teams and keep them focused on doing their best work. Git also makes it possible to align experts across a business to collaborate on major projects.

### Repository

A repository (or Git Project) encompasses the entire collection of files and folders associated with a project, along with each file's revision history. 

The file history appears as snapshots in time called **commits**.

Commits exist as a linked list relationship and can be organized into multiple lines of development called **branches**.

Repositories are self-contained units and anyone who owns a copy of the repository can access the entire codebase and its history

A repository also allows for:

* Interaction with the history
* Cloning
* Creating branches
* Committing
* merging
* Comparing changes across versions of code

Repositories also keeps development projects organized and protected as developers can fix bugs and create new features without fear of derailing mainline development efforts.

## Basic Git Commands

### `git init`

Initializes a brand new Git repository and begins tracking an existing directory. It adds a hidden subfolder within the existing directory that houses the internal data structure required for version control

### `git clone`

Creates a local copy of a project that already exists remotely. The clone includes all the project's files, history, and branches

### `git add`

Stages a change. it tracks changes to a developer's codebase, but it's necessary to stage and take a snapshot of the changes to include them in the project's history. 

The command performs staging. Any changes that are staged will become part of the next snapshot and a part of the project's history. 

Staging and committing separately gives developers complete control over the history of their project without changing how they code and work.

### `git commit`

Saves the snapshot to the project history and completes the change-tracking process. 

It is like taking a photo. Anything that's been staged with `git add` will become a part of the snapshot with `git commit`

### `git status`

Shows the status of changes as untracked, modified, or staged.

### `git branch`

Shows the branches being worked on locally

### `git merge`

Merge lines of development together. Typically used to combine changes made on two distinct branches. 

Ex: A developer would merge when they want to combine changes from a feature branch into the main branch for deployment.

### `git pull`

Updates the local line of development with updates from its remote counterpart. Developers use this command if a teammate has made commits to a branch on a remote, and they would like to reflect those changes in their local environment.

### `git push`

Updates the remote repository with any commits made locally to a branch

## GitHub

GitHub is a Git hosting repository that provides developers with tools to ship better code through command line features,, issues (threaded discussions), pull requests, code review, or the use of a collection of free and paid apps in the GitHub marketplace.

### How GitHub Works

Work is organized into repositories, where developers can outline requirements or direction and set expectations for team members. 

Then, using GitHub flow, developers simply create a branch to work on updates, commit changes to save them, open a pull request to propose and discuss changes, and then merge pull requests once everyone is on the same page

#### The GitHub Flow

The GitHub flow has six steps:

1. **Create a Branch: **Topic branches created from the canonical deployment branch (usually `main`), allows teams to contribute to many parallel efforts.
2. **Add Commits: **Snapshots of development efforts within a branch create safe, revertible points in the project's history
3. **Open a Pull Request: **Pull requests publicize a project's ongoing efforts and set the tone for a transparent development process
4. **Discuss and Review Code: **Teams participate in code reviews by commenting, testing, and reviewing open pull requests
5. **Merge: **Upon clicking merge, GitHub automatically performs the equivalent of a local `git merge` operation. GitHub also keeps the entire branch development history on the merged pull request
6. **Deploy: **Teams can choose the best release cycles or incorporate continuous integration tools and operate with the assurance that code on the deployment branch has gone through a robust workflow