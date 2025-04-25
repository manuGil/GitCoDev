# LESSON 3: Collaborative Software Development
Lecture notes for the lesson on introduction to collaborative software development. 

:::{card} Learning Objectives:

- Collaborate on software projects using one of the Git repository platforms such as GitHub.
- Understand the principles of managing research software projects.
- Organise a software development team by assigning roles and responsibilities.
- Contribute to the development of research software using a collaborative approach.
- Understand the difference between centralised and shared collaborative workflow and when to use them.
- Contribute to open or close software projects using features such as issues, code changes, and pull/merge requests.

+++
Materials:

* [Collaborative software development](https://docs.google.com/presentation/d/1yBy_4r9aHhsUH9AH1s7zLWIQ_h20xNKVYM1somPnz1Q/edit?usp=sharing): a presentation general information about the lesson and illustrations for supporing the explanations of some of the concepts, and exercises.
* [Username form](https://forms.gle/asj6dAhTh6vcyUhV9): a Google form to collect users-names of the collaborative platform that participants will use during the lesson.
:::


## Preparation

:::{admonition} Instructor's Note 
:class: tip
The instructor must collect particiapant's user names for GitHub/Gitlab the day before, so that they can be invited to collaborative repositories. The **username form** above could be use for that.
:::


## i. Recapitulation Operations with Remotes 
**[5 min]**

Common operations with remotes

:::{admonition} Instructor's Note
:class: tip
* Recap slide on how local repostories and remotes are connected and how to work with remotes (Slides).
* Recap what `clone, fetch, merge, pull` and `push` commands do.
:::

## Episode 1: Collaborative Platforms

### 3.1.1. Connecting to Code Repositories  
**[10 min]**

* Ask participants using Windows not to start Git Bash clicking on the desktop icon, as they did in Lesson 1. Instead,
    * use the app menu (the Windows logo)
    * pick up Git Bash from the list
    * launch Git Bash with the option **Run as administrator** available from the drop-down submenu.
    The participants need to type in their credentials as local administrators.
This gain authority to have SSH installing its own features in their laptop next.

:::{admonition} Instructor's Note
:class: tip
At their very first `git push`, Git might complain about a mismatch between the credentials of local and global administrator.
The warning itself suggests another Git command as the remedy to this impasse.
:::

#### Setting up SSH connection for GitHub

:::{admonition} Instructor's Note
:class: tip
GitHub requires authentication via SSH to do pulls and pushes, but not for cloning. **Use slides** to explain what a SSH connection entitles.
:::

* Ask participants to test the connection with:
    ```shell
        ssh -T git@github.com
    ```

* To connect via SSH do the following:

    1. Create a Key-pair inside the `.ssh`  in the Home directory
        ```shell
            # move to Home directory
            cd ~
            # create key
            ssh-keygen -t ed25519 -C "your_email@example.com"
            # save to the default location and file name: ~/.ssh/id_ed25519
        ```

    2. Check the keys have been created
        ```shell
            ls ~/.ssh/
        ```

    3. Start the `ssh-agent` and add private key to agent:
        ```shell
            # start agent
            eval "$(ssh-agent -s)"

            # add private key
            ssh-add ~/.ssh/id_ed25519
        ```
    4. Instruct SSH to use key files in different locations:
        ```shell
            ssh -i <path/private/keyfile>
        ```

    :::{admonition} Instructor's Note
    :class: tip
    Window's user would need to set up the *ssh-agent** to [start the automatically](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows)
    Mac and Linux user don't have to worry about this.
    :::
5. Copy public key to GitHub:
    ```shell
        clip < .ssh/id_ed25519.pub
    ```

:::{admonition} Instructor's Note
:class: tip
Go to GitHub, explain the basics of the interface and
:::

6. add the SSH key.
    ```shell
        Profile > Settings > SSH and GPG keys > New SSH key > Add SSH key
    ```

7. Test SSH connection
    ```shell
        ssh -T git@github.com
    ```

:::{admonition} Instructor's Note
:class: tip
The message for a successful outcome is friendly and plain.Ask participants whether git@github.com has welcomed them.

* More information on working with [SSH keys and GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).
* Check the info on [Troubleshooting SSH for GitHub](https://docs.github.com/en/authentication/troubleshooting-ssh).
:::

#### 2. Publishing Local Repository to GitHub 
**[5 min]**

1. Create GitHub Repo: Go to Github and create an public empty repository called `workshop`. Repo description: *workshop on collaborative development*

2. Add Remote to Local Repo: before this remove any existing remotes in the repository with: `git remote remove <name>`

Move back to the repo directory: `~/Desktop/`
In your local repository (on the terminal), add the remote repository and push the content.

* Connect to remote
    ```shell
        git remote add origin git@github.com:<user-name>/<repo-name>.git
    ```

* Check that remote was added
    ```shell
        git remote -v
        git branch -M main # [Optional if config was changed. This will change the name of the main branch of the repo to make it more friendly]
        git push -u origin main
    ```

#### 3. Check the Content's Repositoy is in GitHub
Go back to your repo page and refresh the browser.

:::{admonition} Instructor's Note
:class: tip
Questions?
:::

### 3.1.2. Exploring the GitHub GUI 
**[5 min]**

Collaborative platform host and manage remote repositories to enable collaborative development.

:::{admonition} Instructor's Notes
:class: tip
Ask participants if they are familiar with GitHub. If not, give a short explanation of what it is for how to explore the GUI.

Mention GitLab at TU Delft as an alternative for a collaborative platform: https://gitlab.tudelft.nl/
:::

### 3.1.3. Collaborating 
**[5 min]**

Participants are invited as collaborators to the **check-in** repository. Participants must have permission to merge pull requets.

1. Demo on how to invite collaborators using the [check-in repository.](https://github.com/manuGil/check-in)

2. Paticipant accept inviation via email or GitHub GUI.

````{card} 
Exercise 1 --- Startig with Collaboration [10 mins]
^^^    

```{include} exercises/L3-ex01.md
```

````

## Episode 2: Collaborative Development for Research Software

### 3.2.1.   Introduction to collaboration in software projects 
**[5 min]**

:::{admonition} Instructor's Note
:class: tip
* A Quick introduction to collaborative development. Definitions  (Slides).

Developing high quality software requires more than programming and technical skill. Exceptionally good programmers can produce high quality software by themselves. But good programmers will need to collaborate in order to develop complex, high quality software.

* Explain the difference between private and close collaboration.

* When to Aim for a Collaborative Approach?
:::

### 3.2.2 Managing Research Software Projects 
**[2 min]**

:::{admonition} Instructor's Note
:class: tip
Explain why management is important for developing software, the key factors to consider, and recommend a management strategy (slides)

**Key Factors:**
- Purpose
- People
- Time
- Maintenance
:::

### 3.2.3 Organising Research Team for Collaborative Development 
**[3 mins]**

:::{admonition} Instructor's Note
:class: tip
**Rores and Responsibilities**

Describe the responsibilities for each role and why they are important for a research-software development project.

**Roles:**
- Project owner
- Administrator
- Reviewer
- Collaborator

> Questions? [10 min]
:::

````{card} 
Exercise 2 --- Roles and Responsibilities
^^^    

```{include} exercises/L3-ex02.md
```

````

## Episode 3: Collaborative Workflows 

### 3.3.1. Documenting Issues
**[8 min]**

Document and track ideas and tasks in a development project. They facilitate planning, discussing  and tracking the progress of a software project.

:::{admonition} Instructor's Note
:class: tip
Do-along. Instruct participant on how to crate issues in a repository. Participants create issue in their recently pushed repository.
:::

Collaborative workflows are estrategies to organise the work of a development team so that many developers can contribute to a software project. Two common estrategies that use version control and collaborative platforms as leverage are:

- The **branching workflow** and
- The **forking workflow**

(branching)=
### 3.3.2. Centralised workflow: branching

:::{admonition} Instructor's Note
:class: tip
A short explanation on the branching workflow (slides)
:::

````{card} 
Exercise 3 --- Branching workflow 
^^^    

```{include} exercises/L3-ex03.md
```

````

### 3.3.3. Pull requests 
**[5 min]**

```{admonition} Instructor's Note
Ask participant if they already have experience with making pull request.
```

Explain what pull request are, and give a demo.
Then teams follow the steps in the exercise below to create and merge pull requests.


````{card} 
Exercise 3 --- Pull requests [6 min]
^^^    

```{include} exercises/L3-ex04.md
```

````

### 3.3.4. Shared workflow: forking 
**[5 min]**

:::{admonition} Instructor's Note
:class: tip
A short explanation on the fork workflow (slides)
:::

````{card} 
Exercise 3 --- Forking Workflow
^^^    

```{include} exercises/L3-ex05.md
```

````

:::{admonition} Instructor's Note
:class: tip
Ask participants if they have Questions.
:::

## Lesson Summary
**[5 min]**

- SHH is a secure way to connect to Code repositories.
- Collaborative workflows provide a way to organize a team around a software project.
- Workflows: branching (centralized) and forking (shared)
- High quality software requires good planning and management.
- Adopting roles and responsibilities can help teams to organize their work.
