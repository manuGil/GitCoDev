# LESSON 1: Fundamental Operations with Git

Lecture notes on the fundamental operation with Git. A hands-on lesson for introducing version control, tracking changes, and the tracking history. 

```{attention}
At the moment, there are no detail explanations for each of the topics. But we expect the experienced instructor will be able to provide explanations using the topics and code snippets  below.
Accidental errors have been removed, but intended errors have been kept.
After each excercise the instructor should demostrate the solutions. Some of the solutions a missing from this lecture notes.
```

````{note}
The list of commands below has been grouped arbitrarily for readability's sake.
````

## Episode 1: Git repositories for version control

### 1.1.1 Introduction to Git

* Create a directory for the course

```shell
    cd ~/Desktop/
    ls
    mkdir -p 2310-gitcodev/git
    ls
    ls 2310-gitcodev/
```
```shell
    cd 2310-gitcodev/git/
    ls
    pwd
```
* Check which shell is available 

```shell
    echo $SHELL
    echo
```

* Check installed version of Git

``` shell
    git
    git --version
    git version
```

### 1.1.2 Git Command Syntax and Getting Help

```shell
    git help
    git helphelp
    git help help
    git config
    git config --list
```
```shell
    git config --global core.editor nano
    git config --global core.autocrlf input # false for Win
    git config --list
    git help config
```
```shell
    git help glossary
    git help -g
```

### 1.1.3. Creating an Empty Reposiory

``` shell
    pwd
    ls
    echo 'first line'
    echo 'first line' >lines.txt
    ls
```
```shell
    cat lines.txt
    echo 'second line' >>lines.txt
    cat lines.txt 
    git status
    git init                                    #initialise repository
```
```shell
    ls
    ls -a
    ls -aF
    ls -aF .git
    ls
```

## Episode 2: Tracking Changes in Working Documents

### 1.2.1 Tracking Changes with the Index
```shell
    git status 
    git add lines.txt
    git status 
    ls -a .git
    git diff lines.txt
```
```shell
    echo 'third line' >>lines.txt
    cat lines.txt
    git diff lines.txt
    git status 
    git add lines.txt
```
```shell
    git status 
    git add lines.txt
    git status 
    git diff lines.txt
```


````{card} 
Exercise 1 --- Tracking changes with the Index
^^^    

```{include} exercises/L1-ex01.md
```

```{dropdown} Answers

    [No answers yet]

```
````

#### Tracking Directories

```shell
    mkdir directory
    ls
    ls -F
    git status 
    touch directory/emptyfile.txt
```
```shell
    ls -R
    ls -RF
    git status 
    git status -u
    git help status
```
```shell
    git add directory
    git status
```

### 1.2.2 Not Tracking and Stop Tracking

```shell
    history
    history 20
    history 20 >history.log
    cat history.log 
    git status
```
```shell
    echo '*.log'
    echo '*.log' >.gitignore
    git status
    ls -a
    ls -aF
```
```shell
    git add .gitignore
    git status 
    echo 'lines.txt' >>.gitignore
    cat .gitignore
```
```shell 
    git status 
    git add .gitignore 
    git status 
```
#### Ignore Untracked Directories

```shell
    touch directory/trackme.txt
    touch directory/donttrackme.txt
    ls directory/
    git status 
    echo 'directory' >> .gitignore
```
```shell
    cat .gitignore 
    git status
    echo '!directory' >> .gitignore
    cat .gitignore 
    git status
```
```shell 
    cat .gitignore 
    echo 'directory' >>.gitignore
    cat .gitignore 
    git status 
    git help gitignore
```
```shell
    git status 
    git add .gitignore 
    git status 
```
```shell
    git rm --staged directory/emptyfile.txt
    git rm --cached directory/emptyfile.txt 
    git status 
    ls -FR
```


````{card} 
Exercise 2 --- Stop tracking Changes in a File
^^^    

```{include} exercises/L1-ex02.md
```

```{dropdown} Answers

    [No answers yet]

```
````

### 1.2.3 Undoing Changes with the Index
```shell
    cat lines.txt 
    echo 'fifth line' >>lines.txt 
    cat lines.txt 
    git status 
    git diff lines.txt
```
```shell
    git restore lines.txt
    cat lines.txt 
    git status 
    git diff lines.txt
    git restore lines.txt
```
```shell
    cat lines.txt 
    git status 
    echo '!directory' >>.gitignore
    ls
    git status 
```
```shell
    git status -u
    git add directory/trackme.txt 
    git status -u
    git add directory/donttrackme.txt 
    git add directory/emptyfile.txt
```
```shell 
    git status 
    git add .gitignore 
    git status 
```

### 1.2.4  Deleting and renaming tracked files and directories

```shell
    git rm --cached directory/donttrackme.txt 
    git status 
    rm directory/
    rm -r directory/
    ls -FR
```
```shell
    git status 
    git restore directory
    git status 
    ls -FR directory/
    touch directory/donttrackme.txt
```
```shell
    git status 
    git rm directory
    git rm -r directory
    git status 
    git rm -rf directory
```
```shell
    git status 
    ls -FR directory/
    git restore directory
    git status 
    git status -u
```
```shell
    mv directory/donttrackme.txt directory/trackne.txt
    git status -u
    # use the command `git mv <oldname> <newname>`
    # lines.txt Lines.txt
    git status -u
    git mv lines.txt Lines.txt
    git status -u
```

````{card} 
Exercise 3 --- Renaming Tracked Files
^^^    

```{include} exercises/L1-ex03.md
```

```{dropdown} Answers

    [No answers yet]

```
````

## Episode 3: Organizing Tracked Changes in a History

### 1.3.1 Commiting Changes with a Configured Identify and a Message

```shell
    cat Lines.txt 
    git diff
    git status 
    git commit -m 'Add first four lines' Lines.txt
```
```shell
    git status 
    git log
```


`````{card} 
Exercise 4 --- Commit Changes in a Tracked File
^^^    

````{include} exercises/L1-ex04.md
````

````{dropdown} Answers    
```shell
    git status 
    git commit -m 'Add .gitignore' .gitignore 
    git status 
```
```shell
    rm -r directory  # to keep things clean
    git status 
    ls
    git log
```
````
`````


`````{card} 
Exercise 5 --- Follow the state of the repository in the commit routine
^^^    

````{include} exercises/L1-ex05.md
````

````{dropdown} Answers    
```shell
    # Procedure for exercise 5
    echo 'fifth line' >>Lines.txt 
    cat Lines.txt 
    git status 
    git add Lines.txt 
    git status
```
```shell 
    git commit -m 'Add fifth lines' Lines.txt 
    git status 
    history
    git log
```
````
`````

### 1.3.2 Inspecting Changes Using the History


`````{card} 
Exercise 6 --- Follow the state of the index in the commit routines
^^^    

````{include} exercises/L1-ex06.md
````

````{dropdown} Answers    

```shell
    # procedure for exercise 6
    git status 
    git diff
    echo 'sixth line' >>Lines.txt 
    git diff
    git add Lines.txt
```
```shell 
    git diff
    git diff Lines.txt
    git commit -m 'Add sixth line' Lines.txt 
    git diff
    git log
```
```shell
    git log --oneline
    git status 
    echo 'seventh line' >>Lines.txt 
    git diff Lines.txt
    git add Lines.txt
```
```shell 
    git diff Lines.txt
    git status 
    git log --oneline
    git diff HEAD Lines.txt
    git diff e278702 Lines.txt
```
```shell
    git diff HEAD~1 Lines.txt
    git log --oneline
    git diff 7f2ca Lines.txt
    git diff HEAD~2 Lines.txt
    git diff HEAD~3 Lines.txt
```
```shell
    git diff HEAD~7 Lines.txt
    git diff Lines.txt
    git diff HEAD~3 Lines.txt
    git diff HEAD HEAD~1 Lines.txt
    git diff HEAD~1 HEAD Lines.txt
```
```shell
    git diff HEAD~4 HEAD~2 Lines.txt
    git diff HEAD~3 HEAD~2 Lines.txt
    git log
    # 
    pwd
```
```shell
    git status 
    git log --oneline
    git diff Lines.txt
    git diff HEAD Lines.txt
    git diff HEAD~1 Lines.txt
```
```shell
    git diff HEAD HEAD~1 Lines.txt
    git diff HEAD~1 HEAD Lines.txt
    diff HEAD HEAD Lines.txt 
    git diff HEAD HEAD Lines.txt 
    git diff HEAD~2 HEAD~2 Lines.txt
```
````
`````


`````{card} 
Exercise 7 --- Explore the changes recorded in the history
^^^    

````{include} exercises/L1-ex07.md
````

````{dropdown} Answers    
```shell
    # No answers yet
```
````
`````

> Exercise 8 is an optional exercise about [comparing differences in the history.](./exercises/L1-ex08.md)


### 1.3.3 Undoing Changes with the History

````{note}
This topic involves using `git restore`. Actual commands are missing.
````

### 1.3.4 Marking the History Using Tags

* Lightweight tags

```shell
    git log --oneline
    git tag 'hey'
    git log --oneline
    git log
```
```shell
    git tag 'hey' HEAD~1
    git tag 'hey2' HEAD~1
    git log --oneline
    git tag 'hey3' HEAD~5
    git tag 'hey4' 87ab7b6
```
```shell 
    git log --oneline
    git diff HEAD HEAD~1 Line.txt
    git diff HEAD HEAD~1 Lines.txt
    git diff hey hey2 Lines.txt
    git log --oneline
```
```shell
    git diff hey hey2 Lines.txt
    echo 'eighth line' >>Lines.txt
    cat Lines.txt 
    git status 
    git add Lines.txt
```
```shell 
    git status 
    git commit -m 'Add eighth line' Lines.txt
    git log --oneline
    git tag -d hey1
    git tag -d hey4
```
```shell
    git log --oneline
    git diff hey hey4 Lines.txt
    git log --oneline
    git tag -d hey2
    git tag -d hey
```
```shell
    git tag HEAD~4 v1
    git tag v1 HEAD~4
    git log --oneline
    git tag v2 HEAD~3
    git tag v3 HEAD~2
```
```shell
    git log --onelein
    git log --oneline
    git tag v4 HEAD~1
    git tag v5 HEAD
    git log --oneline
```


`````{card} 
Exercise 9 --- Add lightweight tags to the history
^^^    

````{include} exercises/L1-ex09.md
````

````{dropdown} Answers    
```shell
    # no answers yet
```

````
`````

* Annotated Tags

```shell
    git tag -a
    git tag -a -m 'First annotated tag' 
    git tag -a -m 'First annotated tag' TAG1
    git log --oneline
```
```shell
    git tag
    git show
    git show HEAD~1
    true
```

## Wrap Up

```{note}
Give a short wrap up about what has been learn.
```
