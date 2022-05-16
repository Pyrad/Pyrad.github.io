---
title: Git commands
date: 2022-04-22 17:48:28
categories:
- linux related
tags: git
---

Frequently used git commands

<!-- more -->

1.	Create a git repository

2.	Set the name and email of current git repo user
	Globally
	```shell
	$ git config --global user.name <USER_NAME>
	$ git config --global user.email <EMAIL>
	```
	Locally
	```shell
	$ git config --local user.name <USER_NAME>
	$ git config --local user.email <EMAIL>
	```

3.	To see the existing configurations, use command
	```shell
	$ git config --list
	```
	To get a specific configuration, use command 'git config <CONFIG_NAME>', e.g.
	```shell
	$ git config user.name
	```

4.	To get help, use command like this, 'git help <KEYWORD>', e.g.
	```shell
	$ git help config
	```

5.	Check logs.
	```shell
	# Check last 4 git logs by printing each log in one line
	git log --oneline --graph -4
	# Check last one log, normally
	git log -1
	```
	
6.	If you add a new file which hasn't been tracked before in the repository,
	first you have to put this file into the so-called "staged area", using command below,
	```shell
	git add <FILE_NAME>
	```
	If you have already modified a file which has been tracked before in the repository,
	you also have to put file into the so-called "staged area", using the command below (indeed same as the command above),
	```shell
	git add <FILE_NAME>
	```
	After you have put the file (newly added or already be tracked in repo), you put file(s) into (local) repository using the command below,
	```shell
	git commit
	```
	
7.	If you modify a file, you can tell the difference by the command below,
	```shell
	git diff
	```
	If you have already put the file(s) into the staged area, you will see nothing by 'git diff'.
	This time, you should use the command below to tell the differences,
	```shell
	git diff --cached 
	git diff --staged  --> git version >= 1.61
	```
	Use a tool to check the differences of files,
	```shell
	# full
	git difftool --tool=tkdiff
	# short 
	git difftool -t <tool_name>
	```
	
8.	To see all the differences in current branch and master branch, use command below to output those differences,
	```shell
	git format-patch -M master -o <OUTPUT_DIR>
	```
	
9.	To patch the current branch with `*.patch` files, use command,
	```shell
	git am ~/<SOME_DIR>/*.patch
	```

10.	To create a new branch from current master branch, use command,
	```shell
	git checkout -b <BRANCH_NAME> master
	```
	
11.	To remove/delete a branch (git branch), use command
	```shell
	git branch -d <BRANCH_NAME>
	```
	If there's anything not fully merged, git will stop the deletion. Use force command to do it (if confirmed to delete),
	```shell
	git branch -D <BRANCH_NAME>
	```

12.	One way to remove untracked files is,
	(1) To see all the untracked files,
	```shell
	git clean -n
	```
	Note here the option "-n" is very important, it just shows files untracked, no deleting
	(2) Clean if all the files listed above are supposed to be removed,
	```shell
	git clean -f
	```
	
13.	To remove unstaged files, use commands below,
	(1)	For a specific file use:
	```shell
	git checkout <PATH_TO_FILE_TO_REVERT>
	```
	(2)	For all unstaged files use:
	```shell
	git checkout -- .
	```

14.	Rename a branch
	```shell
	git branch -m <OLD_BRANCH_NAME> <NEW_BRANCH_NAME>
	```

15.	Rebase a branch
	(1)	Switch to a branch which need rebase
	```shell
	git checkout <DEV_BRANCH>
	```
	(2)	Rebase
	```shell
	git rebase master
	```
	
16. Show origin information
	```shell
	$ git remote
	
	$ git remote show origin
	```

17. Move a file
	```shell
	git mv <OLD_FILE> <NEW_FILE>
	```
	By moving files with git, we notify git about two things
	(1) The hello.html file was deleted.
	(2) The lib/hello.html file was created.
	Both facts are staged immediately and ready for a commit. Git status command reports the file has been moved.
	
18. Git aliases
	Equals to 'git checkout'
	```shell
	$ git config --global alias.co checkout
	```
	Equals to 'git branch'
	```shell
	$ git config --global alias.br branch
	```
	Equals to 'git commit'
	```shell
	$ git config --global alias.ci commit
	```
	Equals to 'git status'
	```shell
	$ git config --global alias.st status
	```

19. Create a new branch in local and then push it to the remote (GitHub) and then track it

    ```shell
    # 1. Create a new branch in local
    git branch <NEW_BRANCH_NAME>
    # 2. Get the remote repo name
    git remote
    # 3. Push the new branch to remote repo
    git push <REMOTE_REPO_NAME> <NEW_BRANCH_NAME>
    # Usually remote repo name is 'origin'
    git push origin <NEW_BRANCH_NAME>
    # 4. Connect this new local branch with the new branch just pushed to the remote repo
    git branch --set-upstream-to=origin/<NEW_BRANCH_NAME>
    # 5. After that, modify code and push as usaul
    git add -A
    git commit -m "XXXXX"
    git push (or use git push origin <NEW_BRANCH_NAME>)
    ```

20. Remove files and restore files

    Reference website [git 删除文件与恢复](https://www.jianshu.com/p/c3ff8f0da85e)

    - A file was deleted locally by `shell` commands other than `git` commands, but it was not added to the stage area, use `checkout` option to restore

      ```shell
      # Remove a file locally by shell commands
      rm <FILE>
      # Restore the file
      git checkout -- <FILE>
      ```

    - A file was deleted locally by `shell` commands other than `git` commands, and it **was** added to the stage area, first use `reset` command to rollback the file to the status of locally removed, and then use `checkout` option to restore

      ```shell
      ##### 1st situation
      # Remove a file locally by shell commands
      rm <FILE>
      # Add to staged area (deleted)
      git add <FILE>
      # Rollback
      git reset HEAD <FILE>
      # Restore the file
      git checkout -- <FILE>
      
      ##### 2nd situation
      # Remove a file locally by git command which will add it to staged area (deleted)
      git rm <FILE>
      # Rollback
      git reset HEAD <FILE>
      # Restore the file
      git checkout -- <FILE>
      ```

    - A file was deleted locally either by `shell` commands or `git` commands, and it **was** not only added to the stage area, but also committed to local repository, then we need to use `reset --hard <ID>` to rollback (ID is got by using `git log` command)

      ```shell
      ##### 1st situation
      # Remove a file locally by shell commands
      rm <FILE>
      # Add to staged area (deleted)
      git add <FILE>
      # Commit
      git commit -m "Delete a file"
      # Get the version ID by using the log option
      git log --pretty=oneline
      # Rollback
      git reset --hard <ID>
      
      ##### 2nd situation
      # Remove a file locally by git command which will add it to staged area (deleted)
      git rm <FILE>
      # Commit
      git commit -m "Delete a file"
      # Get the version ID by using the log option
      git log --pretty=oneline
      # Rollback
      git reset --hard <ID>
      
      ```

    - A file was deleted locally either by `shell` commands or `git` commands, and it **was** not only committed to the local repository, but also push to the remote repository (e.g., Github), then following the steps above, and the use `git push -f`to push the restored files back to the remote repository. Note here `-f` is a must, because git doesn't allow lower versions override higher versions.

      ```sh
      ##### 1st situation
      # Remove a file locally by shell commands
      rm <FILE>
      # Add to staged area (deleted)
      git add <FILE>
      # Commit
      git commit -m "Delete a file"
      # Get the version ID by using the log option
      git log --pretty=oneline
      # Rollback
      git reset --hard <ID>
      # Push to remote
      git push -f
      
      ##### 2nd situation
      # Remove a file locally by git command which will add it to staged area (deleted)
      git rm <FILE>
      # Commit
      git commit -m "Delete a file"
      # Get the version ID by using the log option
      git log --pretty=oneline
      # Rollback
      git reset --hard <ID>
      # Push to remote
      git push -f
      ```

      

