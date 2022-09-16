* As a DevOps Engineer we would be developing lot of stuff to automate the deployment and to store that work we need to know about Version Control Systems (VCS).

* Version control, also known as source control, is the practice of tracking and managing changes to software code.

* VCS are sometimes known as SCM (Source Code Management) tools or RCS (Revision Control System).

* Types of Version Control System:

	1. Local Version Control Systems:

		--> It is one of the simplest forms and has a database that kept all the changes to files under revision control.
		--> It keeps differences between files in a special format on disk.

	2. Centralized Version Control Systems:

		--> It contain just one repository and each user gets their own working copy. 
		--> You need to commit to reflecting your changes in the repository. It is possible for others to see your changes by updating. 
		--> Two things are required to make your changes visible to others which are: 
 				==> You commit
				==> They update
		--> The most obvious is the single point of failure that the centralized repository represents if it goes down during that period collaboration and saving versioned changes is not possible. 
		--> What if the hard disk of the central database becomes corrupted, and proper backups haven't been kept? You lose absolutely everything. 

    3. Distributed Version Control Systems:

		--> It contain multiple repositories. Each user has their own repository and working copy. 
		--> To make your changes visible to others, 4 things are required: 
 			==> You commit
			==> You push
			==>They pull
			==> They update

* One of the most popular VCS tools in use today is called Git. Git is a Distributed VCS, a category known as DVCS, more on that later. Git is free and open source.

* Initialize a repository
```
git init
```

* Configuring git
```
git config --global user.name 'qtdevops'
git config --global user.email 'qtdevops@gmail.com
```

* Three Areas of Git
	1. Working Tree
	2. Staging Area
	3. Local Repository

* Tracked files - Part of version control i.e. local repo

* UnTracked - New file which is not a part of version control i.e. local repo 
* To remove the modified changes from the working tree(unstaged) before adding 
  ```
  git checkout filename
  ```

* Log - History of commit(user's log)
```
git log
git log --oneline
```

* Reset - To move the changes from staging area to working tree / Unstaging / To remove the changes from modified file
```
* git reset --hard HEAD~i 
	* To clean/remove all the changes done in working tree as well as staging area.
 	* will remove all the changes made after that particular version nd moves the head and master position to that particular version (use this command only whem we have remote repo)
	* to get back the lost versions use Reflog command
git reset --soft HEAD~i 
	* will move the changes committed after that particular version to the 	staging area
git reset --mixed HEAD~i 
	* will move the changes added after that particular version to the working tree
```
* Empty directory cannot be added to git version by default.

* Reflog - Git maintains a log on its own for all the changes you make in your local repo

* Checkout - in Initial branch (master) => To remove or revert the changes from working tree / Move head to the previous commit 
	git checkout <commitid> - moves the head position to particular id but the master pointer will be at the latest version 
    git checkout master - moves to the latest version
                        - After creating branch, it is used to switch between branches
	git checkout -b <branch_name> - To create new branch and move the head to new branch

* Restore - Moving the changes from staging area to working and cleaning the working tree but we cannot go for history. For unstage we use following command. We can use same command for discard the changes in working tree also.
```
git restore --staged <file>
```

* Diff - Takes two input data sets and outputs the changes between them

* Clean - To remove the untracked files from your working tree

* rm - remove the file(changes)

--->Staging area also called as Index

--->Head is a pointer which always at the latest version in local repo
 
--->In Git when we initalize a repository a default branch called as master gets created

--->Garbage collection is git's internal mechanism to remove unnecessary changes from .git folder
 
* Merge - Join two or more development histories together
```
git merge <branch what has to be merged>
```
* When we merge the code, we might get merge conflicts, It is upto the user who is merging to resolve conflicts.
* we have two options to resolve the conflict
  * Undo the merge
  ```
  git reset --merge
  ```
  * fix the merge
    * after fixing the conflit add and commit the changes.
--->If the head points to a commit id rather than branch. This state is called as Detached HEAD

* commit --amend: 
  * This command is used to rewrite the spelling mistakes in latest version.
  * Mistake is done in latest commit message.

* **Rebase** - specializes in changing from one branch to other
   ```
   git rebase -i <Head~position> - To fix the changes in the history
   ```
  * pick <commit> = use commit
  * reword  <commit> = use commit, but edit the commit msg
  * edit  <commit> = use commit, but stop for ammending
  * squash <commit> = use commit, but meld into previous commit
  * fixup <commit> = like squash, but discard the commit's log message
  * exec <command> = run command the rest of line using shell
  * break = stop here (continue rebase later with git rebase --continue)
  * drop <commit> = remove commit
  * label <label> = label current HEAD with a name
  * reset <label> = reset head to a label

* A bare repository will have only .git folder and it doesn't have the working tree

* Cherry picking:
	It is the act of picking a commit from a branch and applying it to another.

* Hashing is the process of converting a given key/text (any length) into another smaller value (fixed size string or number).
 
* Hashing algorithms:
		--> md5
		--> SHA1
		--> SHA256

* Git Use SHA1 hashing to track contents

* git cat-file -p <commit id> --> is to know the content of that particular id.

* Self Hosted Remote Repositories:
		--> Gitolite
		--> Git lab Self Hosted
		--> Bit Bucket Self Hosted

* Cloud Hosted or Provider Hosted Remote Repositories:
		--> GitHub
		--> Gitlab
		--> BitBucket
		--> Azure Source Repos
		--> AWS Code Commit

--> Git attributes define the paths so that git treats the files as binary or text and what language to use for syntax highlighting.

--> To create git attributes in the repo we will create ".gitattributes"

--> A gitignore file specifies intentionally untracked files that Git should ignore.

--> ".gitignore" file is created to create a ignore specification.

* git clone:
  * The command creates a copy (or clone) of an existing git repository. Generally, it is used to get a copy of the remote repository to the local repository.

* git config:
  * Command is a convenient way to set configuration options for defining the behavior of the repository, user information and preferences, git installation-based configurations, and many such things. 

* Considered to be easy to work on Git:
  * With the help of git, developers have gained many advantages in terms of performing the development process faster and in a more efficient manner. Some of the main features of git which has made it easier to work are:
    * Branching Capabilities
    * Distributed manner of development
    * Pull requests feature
    * Effective release cycle

* git stash:
  * Git stash can be used in cases where we need to switch in between branches and at the same time not wanting to lose edits in the current branch. 
  * Running the git stash command basically pushes the current working directory state and index to the stack for future use and thereby providing a clean working directory for other tasks.

* Deleting a branching scenario occurs for multiple reasons. One such reason is to get rid of the feature branches once it has been merged into the development branch.

* "git remote" command creates an entry in git config that specifies a name for a particular URL. Whereas "git clone" creates a new git repository by copying an existing one located at the URL.

* "git stash apply" command is used for bringing the works back to the working directory from the stack where the changes were stashed using git stash command.
* This helps the developers to resume their work where they had last left their work before switching to other branches.
* "git stash pop" command throws away the specified stash (topmost stash by default) after applying it.
* "git stash apply" command leaves the stash in the stash list for future reuse. In case we wanted to remove it from the list, we can use the git stash drop command.
* git stash pop = git stash apply + git stash drop

* git annotate:
  * This command annotates each line within the given file with information from the commit which introduced that change. This command can also optionally annotate from a given revision.
  * Syntax: git annotate [<options>] <file> [<revision>]

* "git branch --merged" helps to get the list of the branches that have been merged into the current branch.
* "git branch --no-merged" lists the branches that have not been merged to the current branch.

Resolve conflict in Git:
------------------------
* Conflicts occur whenever there are multiple people working on the same file across multiple branches. 
* In such cases, git won't be able to resolve it automatically as it is not capable of deciding what changes has to get the precedence.
* Following are the steps are done in order to resolve git conflicts:
  1. Identify the files that have conflicts.
  2. Discuss with members who have worked on the file and ensure that the required changes are done in the file.
  3. Add these files to the staged section by using the git add command.
  4. Commit these changes using the git commit command.
  5. Finally, push the changes to the branch using the git.























Adding people to your organization:
-----------------------------------
* In the top right corner of GitHub Enterprise Server, click your profile photo, then click 
  1. Your organization
  2. People
  3. Add member
  4. Invite
  5. choose an organization role for the user : Member
												Owner
				 
  6. choose the license
  7. add the user to teams in the organization.

--> Please run command to push only single file push to git
     ```
	$ git commit -m "Message goes here" filename
     ```

--> Set the date of the last commit to the current date
GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"

Set the date of the last commit to an arbitrary date
GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"

Set the date of an arbitrary commit to an arbitrary or current date
Rebase to before said commit and stop for amendment:

git rebase <commit-hash>^ -i
Replace pick with e (edit) on the line with that commit (the first one)
quit the editor (ESC followed by :wq in VIM)
Either:
GIT_COMMITTER_DATE="$(date)" git commit --amend --no-edit --date "$(date)"
GIT_COMMITTER_DATE="Mon 20 Aug 2018 20:19:19 BST" git commit --amend --no-edit --date "Mon 20 Aug 2018 20:19:19 BST"
See here for more information around rebasing and editing in git: Split an existing git commit.

Following any of these 3 options, you will want to run:

git rebase --continue
