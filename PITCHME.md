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
Initialized empty Git repository in /home/ben/Repo/.git/
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
@[14-22] (Show the tracked files to be commited using "git status"
---
@title[Commit tracked files]
### Commit tracked files

```shell
/Repo$git commit 
/Repo$git commit -m "Added line x"
[master (root-commit) 03e0554] Added line x
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```
@[1] (Commit the changes/tracked files. This will prompt you to add a commit message)
@[2] (You can add the commit message automatically using "-m")
@[3-5] (You'll see this output on your initial commit)
---
@title [Remote repository]
### Adding a remote bits repository

```shell
/Repo$git config --list
credential.helper=osxkeychain
/Repo$git remote add origin git@bits.example.com:britchey/Test.git
/Repo$git remote -v
origin git@bits.example.com:britchey/Test.git (fetch)
origin git@bits.example.com:britchey/Test.git (push)
```
@[1] (bits uses IP whitelisting and pubkey authentication)
@[1-2] (You'll need to be on the Linode IP/VPN and have your public key available to git)
@[3] (With bits you'll want to use the SSH syntax for connecting to the remote repo)
@[4-6] (You can add multiple remote repositories specified by name)
---
