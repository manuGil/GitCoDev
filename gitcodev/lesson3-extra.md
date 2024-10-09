# LESSON 3 EXTRA: Collaborative Software Development
Lecture notes for the lesson on introduction to collaborative software development. These notes contains the following pointers for the instructor:

* Numbers between `[]` are indicative of how much time should be spend in each topic or exercise to keep in track with the lesson [schedule.](schedule.md)
* The text in  **Instructor note** contain explanations or reminders for the instructor. For example:
    `````{admonition} Instructor's Note

    An SSH key must be set to push changes to a remote repository in GitHub.
    ````` 

````{card} 
Presentation 
^^^    

This contains general information about the lesson and illustrations for supporing the explanations of some of the concepts, and 

*[Collaborative software development](https://docs.google.com/presentation/d/1yBy_4r9aHhsUH9AH1s7zLWIQ_h20xNKVYM1somPnz1Q/edit?usp=sharing)*

````

## Preparation

````{admonition} Instructor's Note 
The instructor must collect particiapant's user names for GitHub/Gitlab the day before, so that they can be invited to collaborative repositories.
We recommend a [Google form](https://forms.gle/asj6dAhTh6vcyUhV9), or similar solution.
````

The following helps the instructor to set up a terminal that will show the history of command from one terminal in another. This helps participant to keep track of what commands have been typed by the instructor.  

1. On main terminal:
```bash
 export PROMPT_COMMAND="history -a; $PROMPT_COMMAND"
```
2. On second (history) terminal:
```bash
 tail -f ~/.bash_history | nl -w 3
```

### Windows Terminal (Preview) 
Shortcuts for the Windows Terminal (Preview) App on Windows 11.

| Action             | Shortcut                |
|--------------------|--------------------------|
|Split pane horizontally | Alt + Shift + `-`   | 
|Split pane vertically   | Alt + Shift + `+`   |
|Close a pane            | Ctrl+Shift + `w`     |
|Move pane focus         | Alt + `Arrow keys`   |
|Resize the focused pane | Alt+Shift + `Arrow keys` |


### MacOS Terminal
Shortcuts for the terminal in MacOS

| Action             | Shortcut                |
|--------------------|--------------------------|
|Split pane horizontally | Cmd + `d`   | 
|Close a pane            | Shift + Cmd + `d`   |
------

## i. (Extra) Operations with Remotes 
**[30 min]**

### i.1 Create and explore a bare repository

This section starts with new repositories.


```shell
pwd                           # observe
cd ..                         # directory of the workshop
pwd                           # verify
ls -F                         # observe
git init --bare git-zero.git  # new long option
```
```shell
ls -F git-zero.git            # verify
ls -Fa git                    # observe
ls -Fa git/.git               # observe
cd git-zero.git               # directory of the bare repository
git status                    # observe (fails).
```

```{admonition} Instructor's Note
A bare repository is a special type of Git repository without a *working tree/directory*.
"A bare Git repository is intended to be used as a remote repository where code is shared between members of the team. The bare Git repository is not intended for local development." -- [source: blogpost](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/What-is-a-bare-git-repository)
```

### i.2 Cloning and pushing to "remote" bare repositories (upstreams)

```shell
cd .. # return to workshop directory
git clone git-zero.git git-one                    # new command
ls -Fa git-one                                    # observe
# ls -Fa git-one/.git                               # observe
ls -F                                             # observe
cd git-one                                        # directory of the first clone
```
```shell
git status                                        # observe
# git branch                                        # observe
# git log                                           # observe (fails)
git remote                                        # new command
git remote -v                                     # new short option
```
```shell
echo 1 >> numbers.txt                              # routine
cat numbers.txt                                   # verify
git status                                        # routine with git status
git add numbers.txt                               # routine with git status
git status                                        # routine with git status
```
```shell
git commit -m 'git-one: add first 1' numbers.txt  # routine with git status
git log --oneline                                 # verify
git status                                        # verify (ignore the but-warning)
git push                                          # new command
git status                                        # verify
```
```shell
cd ../git-zero.git                                # directory of the upstreamgit
git status                                        # observe (fails)
git log                                           # observe
# ls -F                                             # observe
cd ..                                             # in the workshop directory
```
```shell
pwd                                               # verify
git clone git-zero.git/ git-two                   # known action
ls -F                                             # verify
cd git-two/                                       # in the second clone
ls -aF                                            # verify
cat numbers.txt                                   # observe
```
```shell
git log                                           # observe
git remote -v                                     # observe
echo 2 >>numbers.txt                              # routine
cat numbers.txt                                   # verify
git add numbers.txt                               # routine
```
```shell
git commit -m 'git-two: add first 2' numbers.txt  # routine
git log --oneline                                 # verify
git push                                          # known action
git status                                        # verify
```

### i.3 Fetching and merging (pulling) from upstreams

```shell
cd ../git-one                                      # in the first clone
pwd                                                # verify
git status                                         # verify
git log --oneline                                  # routine
git fetch                                          # new command
```
```shell
git status                                         # routine
git log --oneline                                  # routine
git log --oneline --all                            # routine
cat numbers.txt                                    # routine
```
```shell
# git pull = git fetch + git merge                 # git has compound commands
# git fetch                                          # known action (nothing happens)
git merge                                          # see episode 2.1 (no conflict here)
git log --all                                      # verify
cat numbers.txt                                    # verify
echo 1 >>numbers.txt                               # routine
```
```shell
# on git-one 
cat numbers.txt                                    # routine
git add numbers.txt                                # routine
git commit -m 'git-one: add second 1' numbers.txt  # routine
git log --oneline --all                            # verify
```
```shell
git status                                         # verify
git push                                           # known action
git status                                         # verify
git log --oneline --all                            # verify
```


### i.3 (continued) Resolving conflicts when pushing

```shell
cd ../git-two/  # change repo                      # in the directory of the second clone
ls                                                 # observe
cat numbers.txt                                    # observe
git status                                         # observe
git log --oneline                                  # observe
```
```shell
echo 2 >>numbers.txt                               # routine
# cat numbers.txt                                    # verify
git add numbers.txt                                # routine
git commit -m 'git-two: add second 2' numbers.txt  # routine
git status                                         # verify
```
```shell
git log --oneline                                  # verify
git push                                           # known action with rejection
git fetch                                          # known action
git status                                         # observe message
```

````{admonition} Instructor's Note

"In Git, divergence indicates that the branch you are currently on and the remote branch (in this case, origin/main) have different commits after their last common ancestor. This can happen in several scenarios:"

* You have made commits locally that haven't been pushed to origin/main.
* Someone else has pushed commits to origin/main that you don't have locally.
* A combination of both.

[source: graphite.dev](https://graphite.dev/guides/resolve-git-message-diverged-branch)

````

```shell
# Will the following create a conflict? -> yes
git merge                                          # known action with conflict
git diff                                           # observe
cat numbers.txt                                    # observe
nano numbers.txt                                   # edit the file within the conflict decorations
cat numbers.txt                                    # verify
git status                                         # verify
```
```shell
git add numbers.txt                                # mark resolution
git status                                         # verify
git commit -m 'git-two: conclude merge'            # conclude merge
git status                                         # verify
git log --oneline                                  # verify
```
```shell
git push                                           # known action
git log --oneline                                  # verify
git status                                         # verify
```

````{admonition} Instructor's Note

**Common cases that cause *merge conflicts*:**

1. When people make different changes to the same line of the same file.
2. When a person edits a file, while other person deletes the same file.

````

````{admonition} Instructor's Note
* Recap slide on how local repostories and remotes are connected and how to work with remotes (Slides).
* Recap what `clone, fetch, merge, pull` and `push` commands do.

```{figure} ../img/recap-remotes.png
---
height: 300px
name: recap-remote-operations
---
```
````

----

## Episode 1: Collaborative Platforms

### 3.1.1. Connecting to Code Repositories  
**[10 min]**

* Ask participants using Windows not to start Git Bash clicking on the desktop icon, as they did in Lesson 1. Instead,
    * use the app menu (the Windows logo)
    * pick up Git Bash from the list
    * launch Git Bash with the option **Run as administrator** available from the drop-down submenu.
    The participants need to type in their credentials as local administrators.
This gain authority to have SSH installing its own features in their laptop.

```{admonition} Instructor's Note
At their very first `git push`, Git might complain about a mismatch between the credentials of local and global administrator.
The warning itself suggests another Git command as the remedy to this impasse.
```

#### Setting up SSH connection for GitHub

````{admonition} Instructor's Note
GitHub requires authentication via SSH to do pulls and pushes, but not for cloning. **Use slides** to explain what a SSH connection entitles.
````

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

    3. Start the `ssh-agent` and add private key to agent (Window's users only):
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

    ````{admonition} Instructor's Note
    Window's user need to set up the *ssh-agent** to [start automatically](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases#auto-launching-ssh-agent-on-git-for-windows).
    Mac and Linux user don't have to worry about this.
    ````
5. Copy public key to GitHub:
    ```shell
        clip < .ssh/id_ed25519.pub
    ```

    ````{admonition} Instructor's Note
    Go to GitHub, explain the basics of the interface and how to add an SSH key to their account.
    ````

6. add the SSH key.
    ```shell
        Profile > Settings > SSH and GPG keys > New SSH key > Add SSH key
    ```

7. Test SSH connection
    ```shell
        ssh -T git@github.com
    ```

````{admonition} Instructor's Note
The message for a successful outcome is friendly and plain. Ask participants whether git@github.com has welcomed them.

* More information on working with [SSH keys and GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh).
* Check the info on [Troubleshooting SSH for GitHub](https://docs.github.com/en/authentication/troubleshooting-ssh).
````

#### 2. Publishing Local Repository to GitHub 
**[5 min]**

1. Create GitHub Repo: Go to Github and create an public empty repository called `workshop`. Repo description: *workshop on collaborative development*

2. Add Remote to Local Repo: before this, remove any existing remotes in the repository with: `git remote remove <name>` This is necessary because in Lesson 2, they have added other remotes.

Move back to the root of the repo: `~/Desktop/<path-to-repo>`
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
Go back to your repo page (in GitHub) and refresh the browser.

````{admonition} Instructor's Note
Questions?

````

### 3.1.2. Exploring the GitHub GUI 
**[5 min]**

Collaborative platforms host and manage remote repositories to enable collaborative development.

````{admonition} Instructor's Notes
Ask participants if they are familiar with GitHub. If not, give a short explanation of what it is for how to explore the GUI.

Mention GitLab at TU Delft as an alternative for a collaborative platform: https://gitlab.tudelft.nl/

> Invite participants to the **check-in** repo
````

### 3.1.3. Collaborating 
**[5 min]**

Participants are invited as collaborators to the **check-in** repository. Participants must have permission to merge pull requets.

1. Demo on how to invite collaborators using the [check-in repository.](https://github.com/WorkshopGitcodev/check-in)

2. Paticipant accept inviation via email or GitHub GUI.

`````{card} 
Exercise 1 --- Startig with Collaboration [10 mins]
^^^    

```{include} exercises/L3-ex01.md
```

```{admonition} Instructor's Note
While completing this exercise, many participants will be warned by Git that they have to pull changes before pushing their contribution. 
This situation should be used as a pre-amble to [branching](branching3).
```

````{dropdown} Answers

2. copy template:

```shell
cp ./check-in/template.md ./check-in/<initials><digits>.md
```

3. Add something to the list:

```shell
nano ./check-in/<initials><digits>.md

# Type a few things
# Save and close the file: CTRL + O, CTTL + X
```
4. Commit and push

```shell
git add .
git commit -m 'added things to my list'
git push
```

5. Git will complain  about not being able to push because the remote
has unsynced changes (except for the very first push). An explanation will be given by the instructor. 

````
`````

## Episode 2: Collaborative Development for Research Software

### 3.2.1.   Introduction to collaboration in software projects 
**[5 min]**

```{admonition} Instructor's Note

* An Quick introduction to collaborative development. Definitions  (Slides).

> Developing high-quality software requires more than programming and technical skill. Exceptionally good programmers can produce high quality software by themselves. But good programmers will need to collaborate in order to develop complex, high quality software.

* Explain the difference between open and close collaboration.

* When to Aim for a Collaborative Approach?

```

### 3.2.2 Managing Research Software Projects 
**[2 min]**

```{admonition} Instructor's Note
 Explain why management is important for developing software, the key factors to consider, and recommend a management strategy (slides)

**Key Factors:**
- Purpose
- People
- Time
- Maintenance

Explain the difference between the purpose of a research project an the purpose of software. 
```

### 3.2.3 Organising Research Team for Collaborative Development 
**[3 mins]**

```{admonition} Instructor's Note
**Rores and Responsibilities**

Describe the responsibilities for each role and why they are important for a research-software development project.

**Roles:**
- Project owner
- Administrator
- Reviewer
- Collaborator

> Questions? [10 min]
```

````{card} 
Exercise 2 --- Roles and Responsibilities
^^^    

```{include} exercises/L3-ex02.md
```


```{dropdown} Answers

    No answer are provided for this exercise.

```
````

## Episode 3: Collaborative Workflows 

### 3.3.1. Documenting Issues
**[8 min]**

Document and track ideas and tasks in a development project. They facilitate planning, discussing  and tracking the progress of a software project.

```{admonition} Instructor's Note
Do-along. Instruct participant on how to crate issues in a repository. Participants create issue in their recently pushed repository.
```

Collaborative workflows are estrategies to organise the work of a development team so that many developers can contribute to a software project. Two common estrategies that use version control and collaborative platforms as leverage are:

- The **branching workflow** and
- The **forking workflow**

(branching3)=
### 3.3.2. Centralised workflow: branching

```{admonition} Instructor's Note
A short explanation on the branching workflow (slides)
```

````{card} 
Exercise 3 --- Branching workflow 
^^^    

```{include} exercises/L3-ex03.md
```

```{dropdown} Answers

    No answer are provided for this exercise.

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

```{dropdown} Answers

    No answer are provided for this exercise.

```
````

### 3.3.4. Shared workflow: forking 
**[5 min]**

```{admonition} Instructor's Note
A short explanation on the fork workflow (slides)
```

````{card} 
Exercise 3 --- Forking Workflow
^^^    

```{include} exercises/L3-ex05.md
```

```{dropdown} Answers

    No answer are provided for this exercise.

```
````

```{admonition} Instructor's Note
Ask participants if they have Questions.
```

## Lesson Summary
**[5 min]**

- SHH is a secure way to connect to Code repositories.
- Collaborative workflows provide a way to organize a team around a software project.
- Workflows: branching (centralized) and forking (shared)
- High quality software requires good planning and management.
- Adopting roles and responsibilities can help teams to organize their work.
