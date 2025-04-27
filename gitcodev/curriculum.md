# Curriculum

Version control is an essential tool in software development. It enables the tracking of changes in the code source and the management of multiple versions. Git is a version control system that allows asynchronous development and is currently the most popular version control system. 

Collaborative development is a software development approach that can help researchers organise their software projects, foster collaboration among their peers and create a community around open-source research software.
Researchers involved or expecting to be involved in developing research software can benefit greatly from mastering the basics of collaborative development.


## Prerequisites

Knowledge and experience in using the command-line interface (CLI) with Unix Shell to perform the following tasks:

* to navigate and visualise the content of directories (folders);
* to create, copy, move and delete files and directories;
* to edit files with terminal-based text editors (such as Nano, vim, emacs, etc);
* to visualise hidden files and directories;
* to redirect and append a command output to a file.

## Tools and Materials

* Unix Shell.
* Git.
* GitHub account or account on a similar platform.
* A laptop with administrative privileges running MacOS, Linux or Windows.

(course-units)=
## Course Units

This course is organised into lessons, episodes and topics. The course consists of **Lessons**. 
Each Lesson is divided into **Episodes** and then into **Topics**. The order in which lessons, 
episodes and topic is organised is the result of extensive discussions on the best way to deliver 
the course to an audience with little to intermediate previous experience and knowledge and the 
experience gathered from providing the course to two groups of mostly PhD candidates. 

````{card} Lesson 1: Fundamental Operations with Git 

**Learning Objectives:**

- Understand the basics of version control.
- Use Git to create repositories and commit changes.
- Apply Git operations to track, reverse and delete changes in working documents.
- Organise tracked changes in the Git history.

```{dropdown} Topics
| Episode | Topic |
|:----|:----|
| **1.1** | **Git repositories for version control** | 
|  | Introduction to Git | 
|  | Git command syntax and getting help | 
|  | Creating an empty repository | 
| **1.2** | **Tracking changes in working documents** | 
|  | Tracking changes with the index | 
|  | Not tracking and stop tracking | 
|  | Undoing changes with the index | 
|  | Deleting and renaming tracked files and directories  | 
| **1.3** | **Organising tracked changes in a history** | 
|  | Committing changes with a configured identity and a message | 
|  | Inspecting changes using the history | 
|  | Undoing changes with the history | 
|  | Marking the history using tags | 

```
````

````{card} Lesson 2: Branching and Remote Operations

**Learning Objectives:**
- Understand the concept of branches in Git repositories.
- Apply Git operations to create and merge branches in a local Git repository.
- Understand the concepts of bare and remote Git repositories. 
- Clone and push changes to remote Gir repositories.
- Synchronise changes between local and remote Git repositories.

```{dropdown} Topics
| Episode | Topic |
|:----|:----|
| **2.1** | **Branching** | 
| --- | Create, rename, change, and delete branches | 
| --- | Develop and compare branches | 
| --- | Visualise and merge branches and resolve conflicts | 
| **2.2** | **Operations with remotes** | 
| --- | Create a bare repositories |
| --- | Cloning and pushing to upstreams |
| --- | Syncing changes between repositories |

```
````

````{card} Lesson 3: Collaborative Software Development

**Learning Objectives:**
- Collaborate on software projects using one of the Git repository platforms such as GitHub.
- Understand the principles of managing research software projects.
- Organise a software development team by assigning roles and responsibilities.
- Contribute to the development of research software using a collaborative approach.
- Understand the difference between centralised and shared collaborative workflow and when to use them.
- Contribute to open or close software projects using features such as issues, code changes, and pull/merge requests.

```{dropdown} Topics
| Episode | Topic |
|:----|:----|
| **3.1** | **Collaborative Platforms** |
| --- | Connecting to code repositories |
| --- | Exploring the GitHub GUI |
| --- | Collaborating |
| **3.2** | **Collaborative Development for Research Software** |
| --- | Introduction to collaboration in software projects |
| --- | Managing research software projects |
| --- | Organising research teams for collaborative development  |
| **3.3** | Collaborative Workflows |
| --- | Documenting issues |
| --- | Centralise workflow: branching
| --- | Pull requests
| --- | Shared workflow: forking

```
````


````{card} Lesson 4: Managing Collaboration and Best Practices

**Learning Objectives:**

- Understand the importance of contribution guidelines and best practices to manage collaboration in research software projects.
- Organise a software team independently to work on activities related to collaborative software development.
- Understand the impact of code reviews and best practices on software quality.
- Perform code reviews as part of a research software team.
- Apply best practices when conducting code reviews. 
- Describe best practices related to licensing, citation, semantic versioning, and software releases.

```{dropdown} Topics
| Episode | Topic |
|:----|:----|
| **4.1** |  **Managing collaboration** |
| --- | Code Reviews |
| --- | Contributing Guidelines |
| **4.2** | **Licensing and Citation** |
| --- | Open Source Licenses |
| --- | Software Citation |
| **4.3** | **Releasing Software** | 
| --- | Semantic Versioning |
| --- | Software Releases |

```
````