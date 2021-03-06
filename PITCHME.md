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

### Optional <span class="gold">Config</span>uration settings

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

### <span class="gold">Init</span>ializing a Repository

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
### Git <span class="gold">Status</span>

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

### <span class="gold">Add</span> a file

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
### <span class="gold">Commit</span> tracked files

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
/Repo$git remote add origin1 git@bits.example.com:britchey/Test.git
/Repo$git remote -v
origin1 git@bits.example.com:britchey/Test.git (fetch)
origin1 git@bits.example.com:britchey/Test.git (push)
```
@[1] (With bits you'll want to use the SSH syntax for connecting to the remote repo)
@[2-4] (You can add multiple remote repositories specified by name)
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

### <span class="gold">R</span>e<span class="gold">m</span>ove a remote repository

```shell
/Repo$git remote rm origin
```
@[1] (In case of oops)
---
@title[That's so fetch]
### <span class="gold">Fetch</span> a remote repository
```shell
/Repo$git fetch origin1
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From bits.linode.com:britchey/Test
 * [new branch]      master     -> origin/master
/Repo$ls -a
.	..	.git
/Repo$git checkout master
Branch master set up to track remote branch master from origin.
Already on 'master'
/Repo$ls -a
.	..	.git	test.txt
```
@[1] ('git fetch $repo_name' to fetch the content of a remote repo)
@[2-6] (The output will show you all of the branches being moved to the local repo)
@[7-8] (You won't be able to see any of the content of the branches until you move to that branch)
@[9] (You'll need to 'checkout' a branch before you can access the content)
@[10-11] (You were already on master but it wasn't tracking from the remote repo origin)
@[12-13] (You now have access to the contents of the master branch of the remote repo)
---
@title[Branching]

### Basic <span class="gold">Branch</span>ing

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

### <span class="gold">Branch</span>ing cont...

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

### <span class="gold">Checkout</span> another branch

```shell
/branch$git checkout newbranch
Branch newbranch set up to track remote branch newbranch from origin.
Switched to a new branch 'newbranch'
/branch$ echo "Let's create a new file" > newfile.txt
/branch$git status
On branch newbranch
Your branch is up-to-date with 'origin/newbranch'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	newfile.txt

nothing added to commit but untracked files present (use "git add" to track)
/branch$git add newfile.txt
/branch$ git commit -m "newbranch changes"
[newbranch 715a277] newbranch changes
 1 file changed, 1 insertion(+)
 create mode 100644 newfile.txt
```
@[1-3] (Use the 'checkout' command to move between branches)
@[4] (Make your changes, create new files, edit existing files)
@[5-13] (If you run 'git status' you'll see all of the untracked changes)
@[14] ('git add' to track the modifications)
@[15-18] ('git commit' to commit the changes to the current branch)

---
@title[Merging]

### <span class="gold">Merge</span> branches

```shell
/branch$git checkout master
Switched to branch 'master'
Your branch is up to date with 'Test/master'
/branch$ls
test.txt
/branch$git merge newbranch
Updating 07a4820..715a277
Fast-forward
 newfile.txt | 1 +
1 files changed, 1 insertion(+), 0 deletion(-)
create mode 10644 newfile.txt
/branch$ls
newfile.txt	test.txt
```
@[1] (Move back to the master branch from newbranch)
@[1-3] (You'll get a status update)
@[4-5] (You won't see the changes that were made on the newbranch) 
@[6] ('merge' newbranch with the newfile.txt into the master branch)
@[7-11] (All of the changes will be displayed in the output)
@[12-13] (The master branch now has all the changes from newbranch added/merged.  **Merged not overwritten) 
---
@title[The last branch]
### Creating a branch

```shell
/Repo$git branch newbranch
/Repo$git checkout newbranch
Swtiched to branch 'newbranch'
/Repo$git checkout -b newbranch
```
@[1] (This will create a new branch)
@[2-3] (To access the new branch you'll have to check it out)
@[4] (You can do both steps in one command with the '-b' option)

---
@title[Push it real good]

### <span class="gold">Push</span> to a remote repo

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
@title[Pull Request]

### <span class="gold">Pull Requests</span> using git

#### 1) Fork the source repo in the bits or github interface
#### 2) Add the newly forked repo as the remote repo in git
```shell
git remote add origin git@bits.linode.com:britchey/repo.git
```
#### 3) Fetch the contents of the repo
```shell
git fetch origin
```
---
#### 4) Branch the master 
```shell
git checkout -b newbranch
```
#### 5) Make changes, edit or add files
#### 6) Track the changes
```shell
git add file1, file2
```
#### 7) Commit the tracked changes
```shell
git commit -m "Changes"
```
---
#### 8) Switch back to the master branch
```shell
git checkout master
```
#### 9) Merge the changes in newbranch with the master branch
```shell
git merge newbranch
```
#### 10) Push the updated repo to the remote repo
```shell
git push origin
```
#### 11) Submit the PR request in the bits or github interface 
