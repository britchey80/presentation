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
@title[Global configurations]

### Optional configuration settings

```shell
~#git config --global user.name "britchey"
~#git config --global user.email "britchey@example.com"
~#git config --global core.editor vim
~#git config --global credential.helper osxkeychain
~#cat .gitconfig
[user]
	name = britchey
	email = britchey@example.com
[core]
	editor= vim
[credential]
	helper = osxkeychain
```
@[1-2] (Attaches your information to your activity)
@[3] (Add a default text editor, vim! or emacs nano...eh)
@[4] (You'll need to make sure that git has access to your pubkey to access bits remotely)
@[5-12] (All of your global configurations will be in the .gitconfig file)

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
/Repo$git clone git@bits.example.com:britchey:Test.git
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
@[1-2] (Create a file in the repository or clone from a remote location)
@[3-13] (Show the untracked files using "git status")
@[14] (Use "git add" to track the file)
@[15-23] (Show the tracked files to be commited using "git status")
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
@[1] (Commit the changes/tracked files. This will prompt you to add a commit message using the default editor)
@[2] (You can add the commit message automatically using "-m")
@[3-5] (You'll see this output on your initial commit)
---
@title[Remote repository 1]
### Adding a remote <span class="gold">bits</span> repository

```shell
/Repo$git config --list
credential.helper=osxkeychain
/Repo$git remote add origin1 git@bits.example.com:britchey/Test.git
/Repo$git remote -v
origin1 git@bits.example.com:britchey/Test.git (fetch)
origin1 git@bits.example.com:britchey/Test.git (push)
```
@[1] (bits uses IP whitelisting and pubkey authentication)
@[1-2] (You'll need to be on the Linode IP/VPN and have your public key available to git)
@[3] (With bits you'll want to use the SSH syntax for connecting to the remote repo)
@[4-6] (You can add multiple remote repositories specified by name)
---
@title[Remote repository 2]
### Adding a remote <span class="gold">Github</span> repository

```shell
/Repo$git remote add origin2 https://github.com/britchey80/Test.git
/Repo$git remote -v
origin1 git@bits.example.com:britchey/Test.git (fetch)
origin1 git@bits.example.com:britchey/Test.git (push)
origin2 https://github.com/britchey80/Test.git (fetch)
origin2 https://github.com/britchey80/Test.git (push)
```
@[1] (You can use this https link for github which will prompt you for your username and password)
@[2-6] (If you run "git remote -v" you'll see all of the available remote repos)
---
@title[Remove remote]

### Remove a remote repository

```shell
/Repo$git remote rm origin
```
@[1] (In case you need to remove a remote repository)
---
@title[Push it real good]

### Pushing to a remote repo

```shell
/Repo$git push origin1 master
Counting objects: 3, done.
Writing objects: 100% (3/3), 224 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To bits.linode.com:britchey/Test.git
 * [new branch]      master -> master
```
@[1] (Syntax is git push $remote_repo_name $branch)
@[2-6] (You'll see an output detailing the changes made to the remote repo)
---
@title[Branching]

### Basic Branching

```shell
~$mkdir branch
~$cd branch
/branch$git init
Initialized empty Git repository in /home/ben/branch/.git/
/branch$git remote add origin git@bits.example.com:britchey/Test.git
/branch$git fetch origin
remote: Counting objects: 9, done.
remote: Total 9 (delta 0), reused 0 (delta 0), pack-reused 9
Unpacking objects: 100% (9/9), done.
From bits.linode.com:britchey/Test
 * [new branch]      master     -> origin/master
 * [new branch]      newbranch  -> origin/newbranch
```
@[1-4] (Create a new dir and initialize git)
@[5-6] (Add a remote repository and fetch it)
@[6-12] (You'll see all of the branches associated with the repo listed in the output)
---
@title[Branching cont]

### Basic Branching cont...

```shell
/branch$ls -a
.	..	.git
/bransh$git checkout master
Branch master set up to track remote branch master from origin.
Already on 'master'
/branch$ls -a
.		..		.git		test.txt
```
@[1-2] (You won't see the contents of a branch until you access it)
@[3-5] (You can access a branch using the "checkout" command)
@[6-7] (Now that you're in a branch you'll be able to view and access the associated files)
---
@title[Branching cont1]

### Swinging to another branch

```shell
/branch$git checkout newbranch
Branch newbranch set up to track remote branch newbranch from origin.
Switched to a new branch 'newbranch'
/branch$ls -a
.               ..              .git            test.txt
/branch$ echo "Let's create a new file" > newfile.txt
/branch$git status
On branch newbranch
Your branch is up-to-date with 'origin/newbranch'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	newfile.txt

nothing added to commit but untracked files present (use "git add" to track)
/branch$git add newfile.txt
/branch$git status
On branch newbranch
Your branch is up-to-date with 'origin/newbranch'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   newfile.txti
/branch$ git commit -m "newbranch changes"
[newbranch 715a277] newbranch changes
 1 file changed, 1 insertion(+)
 create mode 100644 newfile.txt
