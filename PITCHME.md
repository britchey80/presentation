@title[Introduction]

# Git
## <span class="gold">Command Line Basics</span>

### A Primer on navigating the Git command line

---
@title[Getting Started]
### Getting Started
<br>
#### Debian
```shell
~$apt-get install git
```
<br>
#### CentOS
```shell
~$yum install git
```
<br>
#### Mac
```shell
~$brew install git
```

---
@title[Make a Repo]

### Creating a Repository

```shell
~$mkdir Repo
~$cd Repo
/Repo$git init
Initialized empty Git repository in /home/ben/Repository/.git/
/Repo$ls -a
. .. .git
/Repo$ls .git/
branches config description HEAD hooks info objects refs
```

@[1-2] (Create a directory for your new Repository)
@[3-4] (Initialize the Repository)
@[5-6] (You'll see the .git directory added)
@[7-8] (In .git you can see all of the files that make up the Repository)
---
@title[Status]
### Git Status

```shell
/Repo$git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track
```
@[1] (Status command)
@[2-6] (Status output will give you the current branch, commit and tracked files)
---
@title[Add a file]

### Adding a file

```shell
/Repo$echo "This is my test file" > test.txt
/Repo$git status
On branch master

Initial commit

Untracked files:
    (Use "git add <file>..." to include in what will be commited)

	test.txt

nothing added to commit but untracked files present (use "git add" to track)
/Repo$git add test.txt
/Repo$git status
On branch master

Initial commit

Changes to be committed:
    (use "git rm --cached <file>..." to unstage)

	new file:    test.txt
```
@[1] (Create a file in the repository)
@[2-12] (Show the untracked files using "git status")
@[13] (Use "git add" to track the file)
@[14-21] (Show the tracked files to be commited using "git status"

 
