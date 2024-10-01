# LESSON 2: Branching and remote operations

This is a summary of the lecture notes for this lesson.
The original list of commands has been edited and decorated with headings corresponding to the [lessons in the curriculum](course-units) more clearly. 
Some commands have been either removed or relocated or added for clarity and help self-study after the lesson.
Accidental errors have been removed, but intended errors have been kept.

The comments after each line are annotations on whether a command/option appears for the first time (**new**) or is a **known action**. 
Else, the annotation recalls why we typed that certain command, for example to **observe** the state of the play (typically before a certain change) or to **verify** the results of a change.
**routine** commands are the typical commit sequence learned in Lesson 1.

The original list of commands is available at this commit [as displayed by GitHub](https://github.com/4TUResearchData-Carpentries/workshop_notes/blob/056617efa8abb7d79ffb3e85b3ac8dbbcaed50e6/Lesson2.md).

````{note}
The list of commands below has been grouped arbitrarily for readability's sake.
````
---

## Learning objectives:

1. Understand the concept of **branches** in Git repositories.
2. Apply Git operations to **create** and **merge** branches in a local Git repository.
3. Understand the concepts of **bare** and **remote** Git repositories.
4. **Clone** and **push** changes to remote Git repositories.
5. **Synchronise** changes between local and remote Git repositories.

---

## Previous lesson
First let’s make sure we’re still in the right directory. You should be in the `root` directory with `Lines.txt` and `history.log` files. Remember that the branch we are located in `main*`. Note that you might need to change the default branch to be called `main`. This might be the default branch depending on your settings and version of git.


```shell
ls
```
Output:
```console
Lines.txt   history.log
```

The `Lines.txt` should contains the following lines:

```shell
❯ cat Lines.txt 
first line
second line
third line
fourth line
sixth line
seventh line
eighth line
```

## Episode 1: Branching


### 2.1.1 Create, rename, change and delete branches

```shell
git branch                     # new command for checking the branches (output: *main)
git branch B1                  # new argument (create new branch)
git branch                     # verify (output: B1, *main)
```
Your newly created branch (here, `B1`) will show up, but your active branch should still be main. Note that feature is just a name. You could also call your branch ``delft``, if you want.

```shell
git status                     # verify (output: On branch master - nothing to commit, working tree clean)
cat Lines.txt                  # verify (ouptut: Lines.txt with eighth line)
```
Lets first explain the following:
- **What are branches?**
<div style="text-align: center;"> <img src="https://book.the-turing-way.org/_images/sub-branch.png" alt="Branches"> <p><strong>Figure 1:</strong> Branches in version control</p> </div>

- **Why we use branches?** ([The Turing Way Community examples 2022](https://lennartwittkuhn.com/version-control-book/misc/references.html#ref-community2022))

- **what are the most common `git branch` flags?**

Lets explore in our terminal with `git branch --help`:

---
* `-r` or `--remote`: Lists only remote branches.
* `-d` or `--delete`: Deletes a specified branch. For example, `git branch -d B1`.
* `-D` or `--force`: Force deletes a branch, even if it has unmerged changes.
* `-m` or `--move`: Renames a branch. For example, `git branch -m old-branch new-branch`.
* `-c` or `--copy`: Creates a new branch by copying an existing branch. For example, `git branch -c existing-branch new-branch`.
* `-v` or `--verbose`: Shows more information when listing branches, including the last commit message.
---

```shell
git branch -m B1 B2            # new short option (rename B1 to B2)
git log --oneline              # verify (notice that B1 is renamed to B2)
git branch -d B2               # new short option (output: Deleted branch B2 (was 8f14e06).)
git log --oneline              # verify (notice that master is the only branch available)
git branch -m main foo       # known action (rename "main" to "foo" branch)
```
Once a branch has created and its not longer needed, it can be deleted. Removing branches that are no longer active helps maintain a clean and manageable branch structure. To delete a branch, you can use the `git branch` command, followed by a `-d` flag:

```shell
git log --oneline              # verify
git branch -d foo              # known action (fails)
```
This should output similar to:

```shell
error: Cannot delete branch 'foo' checked out at '/Users/courses/gitcodev/2310-gitcodev/git/lesson2'
```

You can only delete a branch you are **NOT** currently working on. Since we are on the branch `foo`, we cannot delete it.

```shell
git branch -m foo main         # known action (replace "foo" to "main")
git branch                     # verify
```
```shell
git status                     # verify
git log --oneline              # verify
git branch B1                  # known action (create again new branch B1)
git branch                     # verify
git log --oneline              # verify
```
Lets now change branches with `git switch` git command.

```shell
git switch                     # new commmand (fails - fatal: missing branch or commit argument)
git switch B1                  # new argument: on branch B1
git log --oneline              # verify
git branch B2                  # known action
git log --oneline              # verify
```
```shell
git switch B2                  # known action: on branch B2
git log --oneline              # verify
git switch main                # known action: on branch main
git log --oneline              # verify
```


````{card} 
Exercise 1 --- Get familiar with branches
^^^    

```{include} exercises/L2-ex01.md
```

```{dropdown} Answers

    [Need to be completed]

    ```shell
    (your work)
    git branch                                                          # verify
    git branch -d B1 B2                                                 # known action
    git branch                                                          # verify
    git log --oneline                                                   # verify
    cat Lines.txt                                                       # verify
    ```

```
````


### 2.1.2 Develop and compare branches (C: will change the name as it doesnt match the title with the content)


After the exercise, lets create the following actions in git:

```shell
git status                                                      # observe (nothing to commit, working tree clean)
git branch B1                                                   # known action
git branch B2                                                   # known action
git branch                                                      # on branch main
git status                                                      # routine with git status
```
```shell
echo 'ninth line' >>Lines.txt                                   # routine with git status
git status                                                      # routine with git status
git add Lines.txt                                               # routine with git status
git status                                                      # routine with git status
```
The output you should get is as following:
```shell
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   Lines.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
**Explanation:**

- `On branch main`: This indicates that you are currently on the `main` branch.
- `Changes not staged for commit`: This section lists the changes that have been made to the files in your working directory but have not yet been staged for commit.
- `(use "git add <file>..." to update what will be committed)`: This message suggests that you can use the git add <file> command to stage the changes in the specified file(s) for the next commit.
- `(use "git restore <file>..." to discard changes in working directory)`: This message suggests that you can use the git restore <file> command to discard the changes in the specified file(s) and revert them to the last committed state.
- `modified: Lines.txt`: This indicates that the file Lines.txt has been modified but the changes have not been staged for commit.
- `no changes added to commit (use "git add" and/or "git commit -a")`: This message indicates that there are no changes currently staged for commit. It suggests using git add to stage changes or git commit -a to automatically stage and commit all changes to tracked files.

```shell
git commit -m 'Add ninth line on main' Lines.txt                # output: [main 0e85a39] added ninth line  1 file changed, 1 insertion(+)
```
```shell
git status                                                      # output: On branch main nothing to commit, working tree clean
git log --oneline                                               # verify
git status                                                      # verify
git switch B1                                                   # on branch B1
git status                                                      # verify (nothing to commit, working tree clean)
```
```shell
git log --oneline                                               # verify
git log --oneline --all                                         # new long option
cat Lines.txt                                                   # verify
```
The output of `Lines.txt` should yield:
```shell
first line
second line
third line
fourth line
sixth line
seventh line
eighth line
```
Lets add the *ninth line* on the `Lines.txt`:
```shell
git status                                                      # routine with git status
echo 'ninth line' >>Lines.txt                                   # routine with git status
```

```shell
git status                                                      # routine with git status
git add Lines.txt                                               # routine with git status
git status                                                      # routine with git status
git commit -m 'Add ninth line on B1' Lines.txt                  # routine with git status
git status                                                      # routine with git status
```
```shell
git log --oneline                                               # verify
git log --oneline --all                                         # verify
git log --oneline --all --parents                               # new long option
```
Now, we switch to the `main` branch:

```shell
git switch main                                                 # on branch main
git log --oneline --all                                         # verify
```
Lets suppose we added a new line by mistake:
```shell
echo 'ninth line (duplicate)' >> Lines.txt                      # routine (an intended mistake)
git add Lines.txt                                               # routine
git commit -m 'Add tenth line on main (with mistake)' Lines.txt # routine
cat Lines.txt                                                   # verify
```
The following output should be displayed:
```shell
❯ cat Lines.txt 
first line
second line
third line
fourth line
sixth line
seventh line
eighth line
ninth line
ninth line(duplicate)
```

### 2.1.3 Visualise and merge branches, and resolve conflicts
Git also offers an option for  visualization of branches inside the command line. For that you can use `git log` (introduced in the previous chapter on Git Essentials) with four flags:

```shell
git log --oneline --all                                # explore
git log --oneline --all --parents                      # explore
git log --oneline --all --parents --graph              # explore
git log --oneline --all --graph --decorate             # any change?
```
We should now focus on the output!


lets change the branch now to `B1`:
```shell
git switch B1                                          # on branch B1
cat Lines.txt                                          # verify (Lines.txt should be without duplicate ninth line)
```
Lets add the tenth line on the `Lines.txt` file to show a case of conflict:
```shell
echo 'tenth line on B1' >> Lines.txt                   # routine
git add Lines.txt                                      # routine
git commit -m 'Add tenth line on B1' Lines.txt         # routine
git log --oneline --all --graph                        # verify
```
Lets now switch to the main branch:

```shell
git switch main                                        # on branch main
```
Before committing the changes, we should review differences between versions of the files using `git diff`
```shell
git diff HEAD HEAD~1 Lines.txt                         # Show changes in Lines.txt between the latest commit and the previous commit
git diff main B1 Lines.txt                             # Show changes in Lines.txt between the main branch and branch B1
git diff main B1~1 Lines.txt                           # Show changes in Lines.txt between the main branch and the parent of the latest commit on branch B1
git diff main~1 B1~1 Lines.txt                         # Show changes in Lines.txt between the parent of the latest commit on the main branch and the parent of the latest commit on branch B1
git log --oneline --all --graph                        # Display a graph of the commit history for all branches in a concise format
```
```shell
git status                                             # verify
nano Lines.txt                                         # edit file to fix mistake
cat Lines.txt                                          # verify
git status                                             # verify
git add Lines.txt                                      # routine
```
```shell
git commit -m  'Correct tenth line on main' Lines.txt  # routine
git log --oneline --all --graph                        # routine
cat Lines.txt                                          # verify
```

````{card} 
Exercise 2 --- Explore differences across branches
^^^    

```{include} exercises/L2-ex02.md
```

```{dropdown} Answers

    [No answers yet]

```
````

````{card} 
Exercise 3 --- Commit in a secondary branch
^^^    

```{include} exercises/L2-ex03.md
```

```{dropdown} Answers

    ```shell
    git switch B2                                             # on branch B2
    cat Lines.txt                                             # verify
    echo 'ninth line' >>Lines.txt                             # routine
    echo 'tenth line' >>Lines.txt                             # routine
    git add Lines.txt                                         # routine
    git commit -m 'Add ninth and tenth line on B2' Lines.txt  # routine
    git status                                                # verify
    git log --oneline --all --graph                           # verify
    ```

```
````

**Merging branches**

Lets come back to branch `B1`:
```shell
git switch B1                                             # on branch B1
echo 'eleventh line' >>Lines.txt                          # routine
echo 'twelfth line' >> Lines.txt                          # routine
git diff                                                  # routine
git add Lines.txt                                         # routine
```
```shell
git commit -m 'Add 11th and 12th lines on B1' Lines.txt   # routine
git log --oneline --all --graph                           # routine
```
We now move back to `main` branch:

```shell
git switch main                                           # on branch main
git diff main B1 Lines.txt                                # verify
git merge -m 'Merge development from branch B1' Lines.txt # wrong syntax
```
This `Lines.txt` in the previous `git merge` command is incorrectly specified as the target to merge. Git expects a branch name here, not a file. To merge changes from branch `B1` into the current branch (e.g., `main`), you should use the branch name, not a file name. But lets explore another error:

```shell
git merge -m 'Merge development from branch B1'           # wrong syntax
```
The error message fatal: No remote for the current branch indicates that the current branch does not have a remote tracking branch set up. This means Git doesn't know which remote branch to merge from. To merge changes from a specific branch (e.g., `B1`) into the current branch, you need to specify the branch name:

```shell
git merge -m 'Merge development from branch B1' B1        # right syntax: fails because of conflict
```
When a merge conflict arises, you should not view it as a limitation of Git but rather as a helpful feature. If you try to merge branches with conflicting changes in a file the output looks similar to this:

```shell
Auto-merging Lines.txt
CONFLICT (content): Merge conflict in Lines.txt
Automatic merge failed; fix conflicts and then commit the result.
```

During a merge conflict, you can run `git status` to see which files are in conflict:

```shell
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   Lines.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

You can also check the different file versions with `diff`
```shell
git diff Lines.txt                                        # verify
```
Git will highlight the conflicting parts in the affected file(s), and you must choose the desired changes or modify them to create a consistent version. To do this, open up the file(s) with conflicts in a text editor of your choice, and you’ll see the conflicting sections marked with the following indicators:

* `<<<<<<<`: indicates the beginning of lines that encountered a merge conflict.
* `=======`: shows the break point for comparison.
* `>>>>>>>`: shows the end of the lines with a merge conflict.

The lines between `<<<<<<< HEAD` and `=======` represent the changes that were made in your current branch.


To resolve the merge conflict, you need to manually edit the conflicting sections to the desired state, removing the conflict markers. You might want to keep some changes from your current branch, some from the merged branch, keep only the changes from one branch, or make entirely new changes.

```shell
cat Lines.txt                                             # explore
nano Lines.txt                                            # edit the file within the conflict decorations
```

In this example, the conflict has been resolved by mixing both sets of changes. Parts of the changes from both branches are now present in the file. If you are done you can use git add to stage the resolved changes:
```shell
cat Lines.txt                                             # verify
git diff                                                  # verify
git status                                                # verify
git add Lines.txt                                         # mark resolution
git status                                                # verify
```
```shell
git commit -m 'Merge changes from B1 into main' Lines.txt # conclude merge wrong syntax
git commit -m 'Merge changes from B1 into main'           # conclude merge right syntax
cat Lines.txt 
```
```shell                                            # verify
git status                                                # verify
git log --oneline --all --graph                           # verify
git log --oneline --all --graph --parents                 # verify
```


````{card} 
Exercise 4 --- A first type of merging
^^^    

```{include} exercises/L2-ex04.md
```

```{dropdown} Answers

    ```shell
    # No answers yet
    ```

```
````

## Episode 2: Operations with remotes


### 2.2.1 Create and explore a bare repository

Lets first explain what is a bare repository:

> A bare repository is a repository that doesn't have a working directory. It only contains the .git directory, the directory in which Git stores all its internal data. The main purpose of these repositories is to be a central repository that developers can push to and pull from, so there's no need in having a working directory. Bare repositories are also used in Git hosting services like GitHub and GitLab. In the next several lessons we will learn how to create a bare repository and how to push to it [Stackoverflow forum](https://stackoverflow.com/questions/37992400/what-is-a-bare-repository-and-why-would-i-need-one).

A bare repository is a Git repository that does not have a working directory. It only contains the .git directory, which stores all the version control information.

*Why We Need Bare Repositories?*
- Central Repository:
Bare repositories are typically used as a central repository that multiple developers can push to and pull from. This setup is common in collaborative environments.
- No Working Directory:
Since bare repositories do not have a working directory, they are not intended for direct development work. This prevents accidental changes to the repository's content.
- Git Hosting Services:
Services like GitHub, GitLab, and Bitbucket use bare repositories to manage and host repositories.

```shell
pwd                           # Print the current working directory
cd ..                         # Change to the parent directory (directory of the workshop)
pwd                           # Verify the current working directory
ls -F                         # List files and directories with a trailing '/' for directories
git init --bare git-zero.git  # Initialize a new bare Git repository named git-zero.git
```

```shell
ls -F git-zero.git            # Verify the creation of the bare repository by listing its contents
ls -Fa git                    # List all files and directories, including hidden ones, in the git directory
ls -Fa git/.git               # List all files and directories, including hidden ones, in the .git directory of the git repository
cd git-zero.git               # Change to the directory of the bare repository
ls                            # List all files and directories in the bare repository
```

Lets try to write:
```shell
git status                    # observe (fails)
```
The error message `fatal: this operation must be run in a work tree` indicates that the git status command was run inside a bare repository. The git status command requires a working directory to show the status of files, but bare repositories do not have a working directory. 
**Explanation**
Bare Repository:
A bare repository only contains the version control information and does not have a working directory where files are checked out.
Commands like git status, git log, and others that operate on the working directory or the index are not applicable in a bare repository.


Another:

```shell
git log                       # observe (fails)
```
The error message fatal: your current branch 'master' does not have any commits yet indicates that the git log command was run on a branch that does not have any commits. The git log command displays the commit history, but if there are no commits, it cannot show any history.

```shell
git branch                    # observe its empty
cd ..                         # observe
ls                            # verify
```

### 2.2.2 Cloning and pushing to "remote" bare repositories (upstreams)

This command clones the bare repository `git-zero.git` into a new directory named `git-one`.

```shell
git clone git-zero.git git-one                    # new command
```
You should get the following output:

```shell
❯ git clone git-zero.git git-one 
Cloning into 'git-one'... 
warning: You appear to have cloned an empty repository. done.
```
Since git-zero.git is empty (no commits or files), the cloned repository git-one is also empty.

```shell
ls -Fa git-one                                    # observe
ls -Fa git-one/.git                               # observe
ls -F                                             # observe
cd git-one                                        # directory of the first clone
```
```shell
git status                                        # nothing to commit
git branch                                        # observe that is empty
git log                                           # observe (fatal: your current branch 'master' does not have any commits yet)
```
The git remote command is used to manage the set of repositories ("remotes") whose branches you track. These remotes are typically other repositories that you can fetch from and push to.

```shell
git remote                                        # new command
git remote -v                                     # new short option
```
The command git remote lists the short names of all configured remote repositories. When you run git remote and see origin, it means that there is a remote repository configured with the name `origin`. 

What is `origin`?: origin is the default name given to the remote repository when you clone a repository or add a remote for the first time. It is a shorthand reference to the URL of the remote repository from which you cloned your local repository. You can fetch from and push to this remote repository using the name origin.

```shell
echo 1 >> numbers.txt                              # routine
cat numbers.txt                                   # verify
git status                                        # routine with git status (untracked file: numbers.txt)
git add numbers.txt                               # routine with git status 
git status                                        # routine with git status (changes to be commited: numbers.txt)
```

```shell
git commit -m 'git-one: add first 1' numbers.txt  # routine with git status
git log --oneline                                 # verify
git status                                        # verify (ignore the but-warning)
```
```shell
git push                                          # new command
```
This is the output:
```shell
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 234 bytes | 234.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To /Users/ccugutrillague/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git
 * [new branch]      master -> master
```
**Explanations:**

1. Enumerating objects: 3, done.
Git is identifying the objects (commits, trees, blobs) that need to be pushed to the remote repository.
In this case, there are 3 objects to be pushed.

2. Counting objects: 100% (3/3), done.
Git counts the total number of objects to be pushed.
It confirms that all 3 objects have been counted.
3. Writing objects: 100% (3/3), 234 bytes | 234.00 KiB/s, done.
Git writes the objects to the remote repository.
It shows the total size of the objects (234 bytes) and the speed at which they were written (234.00 KiB/s).
4. Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    - Total 3: Indicates the total number of objects being pushed.
    - delta 0: Indicates that no objects were compressed using delta compression.
    - reused 0: Indicates that no objects were reused from the remote repository.
    - pack-reused 0: Indicates that no objects were reused from a previous pack.
5. To /Users/ccugutrillague/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git
Specifies the remote repository to which the objects are being pushed.
6. `* [new branch] master -> master`
Indicates that a new branch named master is being created on the remote repository.
The local master branch is being pushed to the remote master branch.

```shell
git status                                        # verify
```
```shell
cd ../git-zero.git                                # directory of the upstreamgit
git status                                        # observe (fails)
git log                                           # observe
ls -F                                             # observe
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
```

**Summary of `git remote -v` Output**
- **`origin`** is the remote repository.
- The URL for `origin` is `/Users/../Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git`.
- The URL is used for both fetching and pushing changes.

```shell
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


### 2.2.3 Fetching and merging (pulling) from upstreams

The git fetch command is used to download commits, files, and references from a remote repository into your local repository. It updates your local copy of the remote branches without modifying your working directory or local branches.

**Key Points**
- Fetches Updates: Downloads new data from the remote repository.
- No Changes to Working Directory: Does not change your working directory or local branches.
- Updates Remote Tracking Branches: Updates your local copy of the remote branches (e.g., origin/master).

```shell
cd ../git-one                                      # Change to the directory of the first clone
pwd                                                # Verify the current working directory
git status                                         # Verify the status of the working directory
git log --oneline                                  # View the commit history in a concise format
git fetch                                          # Fetch updates from the remote repository
```
```shell
git status                                         # routine
git log --oneline                                  # routine
git log --oneline --all                            # routine
cat numbers.txt                                    # routine
```
```shell
# git pull = git fetch + git merge                 # git has compound commands
git fetch                                          # known action
git merge                                          # see episode 2.1 (no conflict here)
```
Summary of `git merge` output:
- The `git merge` command successfully merged the changes from the specified branch into your current branch.
- The merge was a `"fast-forward"` merge, meaning no new merge commit was created.
The file `numbers.txt` was modified, with one line added.

```shell
git log --all                                      # verify
cat numbers.txt                                    # verify
echo 1 >>numbers.txt                               # add another 1
```
```shell
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


### 2.2.3 (continued) Resolving conflicts when pushing

```shell
cd ../git-two/                                     # in the directory of the second clone
ls                                                 # observe
cat numbers.txt                                    # observe
git status                                         # observe
git log --oneline                                  # observe
```
```shell
echo 2 >>numbers.txt                               # routine
cat numbers.txt                                    # verify
git add numbers.txt                                # routine
git commit -m 'git-two: add second 2' numbers.txt  # routine
git status                                         # verify
```
```shell
git log --oneline                                  # verify
git push                                           # known action with conflict
```
Expected `git push` output:

```shell
To /Users/[..]/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to '/Users/[..]/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
The error message you received when running git push indicates that your push was rejected because the remote repository contains commits that are not present in your local repository. This situation typically arises when someone else has pushed changes to the remote repository that you do not have locally. 

**Explanation:**

**To /Users/ccugutrillague/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git**
- Specifies the remote repository to which you attempted to push.

**! [rejected] master -> master (fetch first)**
- Indicates that the push was rejected.
- The `master` branch on your local repository could not be pushed to the `master` branch on the remote repository.
- You need to fetch the latest changes from the remote repository first.

**error: failed to push some refs to '/Users/ccugutrillague/Documents/courses/gitcodev/2310-gitcodev/git/git-zero.git'**
- Confirms that the push operation failed.

**hint: Updates were rejected because the remote contains work that you do not have locally.**
- Explains that the remote repository has commits that are not present in your local repository.

**hint: This is usually caused by another repository pushing to the same ref.**
- Indicates that another user or repository has pushed changes to the same branch you are trying to push to.

**hint: You may want to first integrate the remote changes (e.g., 'git pull ...') before pushing again.**
- Suggests that you should fetch and merge the remote changes into your local branch before attempting to push again.

**hint: See the 'Note about fast-forwards' in 'git push --help' for details.**
- Refers you to the Git documentation for more information about fast-forward merges and push rejections.

The reason for rejection is that you need to `fetch` the latest changes from the remote repository first.

**Summary of git push Output**
1. Push Rejected: The push was rejected because the remote repository contains commits that are not present in your local repository.
2. Fetch First: You need to fetch the latest changes from the remote repository and integrate them into your local branch before pushing again.
3. Steps to Resolve: Fetch the latest changes, merge them into your local branch, resolve any conflicts, and then push again.

```shell
git fetch                                          # Fetch updates from the remote repository
git status                                         # Check the status of the working directory
git merge                                          # Merge the fetched changes into your current branch
```
```shell
git diff                                           # Show the differences and conflicts
```
```shell
diff --cc numbers.txt
index 2ca3cd5,e13c5bf..0000000
--- a/numbers.txt
+++ b/numbers.txt
@@@ -1,3 -1,3 +1,7 @@@
  1
  2
++<<<<<<< HEAD
 +2
++=======
+ 1
++>>>>>>> refs/remotes/origin/master
```
```shell
cat numbers.txt                                    # View the contents of numbers.txt
nano numbers.txt                                   # Edit the file to resolve the conflict
cat numbers.txt                                    # Verify the resolved contents of numbers.txt
git status                                         # Verify the status of the working directory
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

````{card} 
Exercise 5 --- Another type of merge
^^^    

```{include} exercises/L2-ex05.md
```

```{dropdown} Answers

    ```shell
    # No answers yet
    ```

```
````


```{dropdown} Differences Between git fetch and git merge?
Key Differences
* `git fetch:` Only downloads updates from the remote repository.
Does not change your working directory or local branches.
Allows you to review changes before merging.
* `git merge:` Merges changes from one branch into another branch.
Directly modifies your current branch by integrating changes from the specified branch.
Typically used to combine feature branches into the main branch.

```