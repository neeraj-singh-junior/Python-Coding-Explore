````
-------------------------------------------------------------------------------------f
-> Title : Git Notes
-> Author: @neeraj-singh-jr
-> Status : Ongoing...
-> Created : 05/12/2022
-> Updated : 03/12/2024
-> Summary : Notes indices are as follows (**** pending)
`-------------------------------------------------------------------------------------
-> Q012 : Remove the Untracked files in git project;;
-> Q011 : Update Remove Repository SSH url link;;
-> Q010 : Reset Head or Go Back & Forth in Commits History;;
-> Q009 : Tags Creation in Git;;
-> Q008 : Rename Command using Git;;
-> Q007 : Create Alias in Git;;
-> Q006 : Show commit logs in Graph Style;;
-> Q005 : Revert Changes from Staged Area ;;
-> Q004 : Difference in Manual Add and Commit with '-am' Flag;;
-> Q003 : Check code changes pulled from origin;;
-> Q002 : Git Favourite Commands;;
-> Q001 : What is Git;;
-------------------------------------------------------------------------------------
````

### GIT NOTES : BEGINNING

-------------------------------------------------------------------------------------
### Q012 : Remove the Untracked files in git project;;

To remove the untracked files from the git project

````
# List untracked files using git;;
$ git clean -n

# Remove untracked file with interaction;;
$ git clean -i

# Forcefully remove untracked file;;
$ git clean -f
````

NOTE: `Checkout` only remove the modified changes only.


-------------------------------------------------------------------------------------
### Q011 : Update Remove Repository SSH url link;; 

This Scenario can be used to update to update the existing remote link with
the newer one. Like this,

````
# Intial SSH URL 
$ git remote add origin git@bitbucket.org:sqrrl-fintech/repo1.git
$ git remote -v

# OUTPUT:
origin	git@bitbucket.org:sqrrl-fintech/repo1.git (fetch)
origin	git@bitbucket.org:sqrrl-fintech/repo1.git (push)
````

#### New SSH URL
````
$ git remote set-url origin git@bitbucket.org:sqrrl-fintech/repo2.git
$ git remote -v

# OUTPUT:
origin	git@bitbucket.org:sqrrl-fintech/repo2.git (fetch)
origin	git@bitbucket.org:sqrrl-fintech/repo2.git (push)
````


-------------------------------------------------------------------------------------
### Q010 : Reset Head or Go Back & Forth in Commits History

`Reset command` is used to move changes back and forth from git commits
timeline. Suppose you've a git timeline is like this,

````
# Commit Timeline, Initially
* ace6055 (HEAD -> master, tag: v1) added c <-- HEAD NOW
* 860ce77 staged commit
* 8172daf 2 files
* 0aab975 author
* 3b6b754 added first file
````

Suppose now you want to go the first commit, but you want to keep the
latest changes. Basically you just want to move point your head on the
first commit then prefer soft reset. Like this,

````
$ git reset --soft 3b6b754

# Commits Timeline, Soft Reset
* ace6055 (tag: v1) added c
* 860ce77 staged commit
* 8172daf 2 files
* 0aab975 author
* 3b6b754 (HEAD -> master) added first files <-- HEAD NOW
````

for this same case, now you want to move all your changes back to the very
first commit changes then prefer the hard reset. In this all the files
structure move back to the first commit changes, But you commits history
will be maintained. Like this, 

````
$ git reset --hard 3b6b754

# Commit Timeline, Hard Reset
* ace6055 (tag: v1) added c
* 860ce77 staged commit
* 8172daf 2 files
* 0aab975 author
* 3b6b754 (HEAD -> master) added first file
````

now suppose you have fixed few changes from the first commit and then you
want to go back to the latest commit then, do the similar step with hard.

````
$ git reset --hard ace6055

# Commit Timeline, Like Initially
* ace6055 (HEAD -> master, tag: v1) added c
* 860ce77 staged commit
* 8172daf 2 files
* 0aab975 author
* 3b6b754 added first file
````

-------------------------------------------------------------------------------------
### Q009 : Tags Creation in Git;;

Tags are use to label the branch tracking the changes till current specific
   requirements.

#### Create Tags:

> $  git tag your-new-tags

or, you can pass message as well

> $ git tag -a v1 -m "your new message"

#### List Tags: 	

> $ git tag --list

#### Delete Tag:

````
# FROM REMOVE REPO:-
$ git push origin :your-remote-tag
````
````
From LOCAL REPO:
$ git tag -d your-local-tag
````

#### Create Tag for a specific Commit:-

> $ git tag -a v1 -m "previous release" ac34522e

#### Create tag for current or any other branch

> $ git tag stable-release master

or, for another branch

> $ git tag unstable-release develop

#### Push tag to Remote Repo 
if you wanted to push all the tags, then this command,

> $ git push --tags

for single tag push, use this command
> $ git push origin tag-name

for eg,
````
$ git push origin stable
$ git push origin unstable
````

#### Renaming Tag in Git

This will rename the git tag.

> $ git tag -f stable master


-------------------------------------------------------------------------------------
### Q008 : Rename & Delete Command using Git;;

NOTE: Even if you have stage the changes then the changes will be reflect
there as well. Renamed file will be shown there.

#### CASE : RENAME COMMAND
Suppose you have file using temp.txt => demo.txt, then and no changes will be
shown, everything will be up to date.

for eg,
````
# you can use this command;
$ git mv temp.txt demo.txt
````

#### CASE : DELETE COMMAND
For deleting a file or stage files, you can use this command

for eg,
````
$ git rm demo.txt
````

-------------------------------------------------------------------------------------
### Q007 : Create Alias in Git;;

Git gives you alias command to make alias for long commands, like this 

Example 1: Git about "your message
````
git config --global --add alias.remark '
	!describe() { 
		msg="$1"; 
		git config branch."$(git branch --show-current)".description ${msg:+"$msg"}; 
	}; describe'
````

Example 2: Add pretty logs in graph style
````
git config --global --add alias.plogs 
	'!describe() {
		git log --oneline --graph --decorate --all;
	}; describe'
````

Example 3: Add alias to show conflicts in files
````
git config --global --add alias.conflicts '
	!describe() { 
		git diff --name-only --diff-filter=u; 
	}; describe'
````


-------------------------------------------------------------------------------------
### Q006 : Show commit logs in Graph Style;;

Use this command to show logs in Graph style,
````
$ git log --oneline --graph --decorate --all
````

-------------------------------------------------------------------------------------
### Q005 : Revert Changes from Staged Area ;;

Suppose you made a few changes in your profile files(a.txt), then

you've added it to staging area
````
$ git add .
````

but now you want to add few more changes to the same commit, then
````
$ git reset HEAD
````

This will revert you stages changes to unstages state.


-------------------------------------------------------------------------------------
### Q004 : Difference in Manual Add and Commit with '-am' Flag;;

#### Case 1 : Manually Add using Git

In this you, manually saying git to add all my changes to staging area

Your changes can include - Modified, Untraced, Updated etc.

You can do so by 
````
$ git add .
$ git commit -m "your-msg"
````

#### Case 2 : Automatic Add using Git

In this case, you are just using commit and add in the same commit command and
saying the git to first add all changes then commit the changes

NOTE: But, here is the important thing to Notice, which is this automatic add
and commit will not in the case. When you've Untraced files in your changes.
In this case it will fail to add the files changes.

````
# You can check if you're file is alread tracked by git or not using below command
# This will list you the tracked files names.
$ git ls-files


# If you 've not Untraced files, then go for it
$ git commit -am "your-msg"
````

-------------------------------------------------------------------------------------
### Q003 : Check code changes pulled from origin;;

Suppose you are on develop branch of your project,

Then proceed as following

// On Terminal

````
# Fetch everything from the remote/develop branch;;
$ git fetch origin develop

# Check the difference using the diff command;;
$ git diff origin/develop 

# If everything ok, then merge 
# make sure u're on develop branch before
$ git merge origin/develop
````


-------------------------------------------------------------------------------------
### Q002 : Git Favourite Commands;;;;

#### GIT FAVOURITE COMMANDS :-

````
// Delete Remote Branch
$ git push origin :branch-name

//--- set upstream for local branch to remote
$ git branch --set-upstream-to origin feature-branch

//--- show up which remote branch a local branch is tracking
$ git branch -v

//--- short version to set upstream with very first push
$ git push -u origin local-branch

//--- fetch and pull branch
$ git fetch origin BAC-2633-transaction-apis-create-lumpsum
$ git checkout BAC-2633-transaction-apis-create-lumpsum

//--- push from different local branch to different remote branch
git push <remote> <branch with new changes>:<branch you are pushing to>
for eg, $ git push origin branch-1:branch-2

//--- fetch origin
$ git fetch --all
$ git pull --rebase origin master

//--- Show local branch sync with remote branch
$ git branch -v

//--- Setup Email for Local Repo:
$ git config --local user.email <your_email>

//--- Clone Single branch from Repo:
$ git clone -b <branch_name> <repo_url>
$ git clone -b <branch_name> --single-branch <repo_url>

//--- view all settings
$ git config --list --show-origin

//--- Global configurations for your git
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
$ git config --global init.defaultBranch main

//--- View all the merge conflicts:
git diff

//--- View the conflicts against the base file
git diff --base <filename>

//--- Preview changes, before merging
git diff <sourcebranch> <targetbranch>
for eg, git diff origin/develop develop

//--- Show all changes made in last commit in any branch;
git show BAC-2667

//--- Add description to a branch;
git branch BAC-2667
git branch --edit-description "NEW BRANCH DESCRIPTION"
or,
git config branch.BAC-2667.description "NEW DESCRIPTION"

//--- Reveal branch description;
git config branch. <branch name>. description

//--- Config level alias with function ~v1;
git config --global --add alias.about '
	!describe() { 
		msg="$1"; 
		git config branch."$(git rev-parse --abbrev-ref HEAD)".description ${msg:+"$msg"}; 
	}; describe' 

//--- Config level alias with function ~v2:
git config --global --add alias.remark '
	!describe() { 
		msg="$1"; 
		git config branch."$(git branch --show-current)".description ${msg:+"$msg"}; 
	}; describe'

//--- Know the name of the branch;
git rev-parse --abbrev-ref HEAD
or,
git branch --show-current

//--- Undo last commit
git reset --soft HEAD^

//--- Undo last commit : KEEP CHANGES;
git reset --soft HEAD~1

//--- Undo last commit : REMOVE CHANGES
git reset --hard HEAD~1

//--- Fetch list of filename changed during git fetch
git fetch && git diff --name-only ..origin/develop
git fetch && git diff --name-only develop develop@{u}

// Copy commit history of one branch to another
git branch -m master main

// Git Restore Stage Changes
git restore --staged <file>...

// Alias to print only conflict files
git config --global --add alias.conflicts '!describe() { git diff --name-only --diff-filter=u; }; describe'

// List number of file changes in Stash
git stash show stash@{0}

// Show the file content difference in Stash
git stash show -p stash@{0}
````

-------------------------------------------------------------------------------------
### Q001 : What is Git;;

Git is a distributed version control system: tracking changes in any set of
files, usually used for coordinating work among programmers collaboratively
developing source code during software development. 

Its goals include speed, data integrity, and support for distributed,
non-linear workflows.


-------------------------------------------------------------------------------------
