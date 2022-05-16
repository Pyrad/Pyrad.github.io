---
title: Multiple Remote Repositories
date: 2022-05-16 21:40:34
categories:
- linux related
tags: git
---

This article explaned how to add 2 remote repositories for a same local git repository

<!-- more -->

# README of multi_remote_repo_test

This repository is used for testing the following

- Create a local git repository, don't link to any remote repository (e.g, Github, Gitee, ...)

- Create some files and commit to this local repository, **still**, for the moment, don't link this local repository to any remote (as above said)

- Still create some files, delete some files, edit some files, ... and commit them to this local repository, repeat again and again, until you don't want to do anymore. **Still**, at this point, don't link this local repository to any remote (as above said)

- Link this to an empty remote repository (this remote repository should have been created from remote, e.g., created in Github), by using `git remote add <repo_name> <url>`

  ```sh
  # Command
  git remote add <repo_name> <url>
  # For example, here now I'm in a local git repo
  # and I created an empty remote repo named multi_remote_repo_test in Github,
  # then I link this local git repo to the remote by sepcifying the name and its URL
  git remote add origin git@github.com:Pyrad/multi_remote_repo_test.git
  ```

- After linking it to the remote (for example, here I first linked it to a Github repository named 'multi_remote_repo_test'), push local changes to the remote for the first time. 
  Since the first time there's no corresponding branch in the remote repository, then we should specify one when before pushing for the first time

  ```sh
  # -*-*-*-*-*-*-*-* Choice 1 -*-*-*-*-*-*-*-*
  # Set remote's branch which corresponds this local repo's current branch
  git branch --set-upstream-to=origin/<BRANCH_NAME>
  # Push to remote
  git push
  
  # -*-*-*-*-*-*-*-* Choice 2-*-*-*-*-*-*-*-*
  # Or directly set upstream when pushing for the first time
  git push --set-upstream origin master
  ```

  

- Still create some files, delete some files, edit some files, ... and commit them to this local repository, **and** push them to the remote just added as shown above, repeat again and again, until you don't want to do anymore.

- Now here's the funny part, add another remote URL for the previous remote name, which means now the same remote name `origin` now corresponds to different remote repositories!!
  Because I add this local repository to the Github as the first remote repository, the `fetch` is from the Github, if you first add this local repository to the Gitee (maybe other remotes), then `fetch` here would be from Gitee.

  ```sh
  git remote set-url --add origin git@gitee.com:pyrad/multi_remote_repo_test.git
  
  # Before add a new url for a same remote name
  Pyrad@SSEA MINGW64 /d/GithubClone/multi_remote_repo_test (master)
  $ git remote -v
  origin  git@github.com:Pyrad/multi_remote_repo_test.git (fetch)
  origin  git@github.com:Pyrad/multi_remote_repo_test.git (push)
  
  # Add a new url for a same remote name
  Pyrad@SSEA MINGW64 /d/GithubClone/multi_remote_repo_test (master)
  $ git remote set-url --add origin git@gitee.com:pyrad/multi_remote_repo_test.git
  
  # After add a new url for a same remote name
  Pyrad@SSEA MINGW64 /d/GithubClone/multi_remote_repo_test (master)
  $ git remote -v
  origin  git@github.com:Pyrad/multi_remote_repo_test.git (fetch)
  origin  git@github.com:Pyrad/multi_remote_repo_test.git (push)
  origin  git@gitee.com:pyrad/multi_remote_repo_test.git (push)
  ```

  

- Since now you just set another URL for this remote name, which means the other remote could now be pushed to, try it

  ```sh
  Pyrad@SSEA MINGW64 /d/GithubClone/multi_remote_repo_test (master)
  $ g push
  Everything up-to-date
  Enumerating objects: 12, done.
  Counting objects: 100% (12/12), done.
  Delta compression using up to 4 threads
  Compressing objects: 100% (8/8), done.
  Writing objects: 100% (12/12), 1.75 KiB | 596.00 KiB/s, done.
  Total 12 (delta 3), reused 0 (delta 0), pack-reused 0
  remote: Powered by GITEE.COM [GNK-6.3]
  To gitee.com:pyrad/multi_remote_repo_test.git
   * [new branch]      master -> master
  ```

  As above shown, for the Github remote repository, everything is up to date and no change to push, but for the Gitee, some changes would be pushed to it.

- Please note that the only `fetch` source here is from the Github, so `git pull` would only pull changes from the Github remote repository. 
  As there are 2 remote repositories for this local repository, each time `git push` would push changes to the 2 different remote repositories at the same time.

- For example, after I made some changes locally and when I do `git push`, I got the following messages. As you could see, the first part of the log said it was pushing changes to **Github**, while the second part of the log means it was pushing changes to **Gitee**, they happened at the same time.

  ```sh
  Pyrad@SSEA MINGW64 /d/GithubClone/multi_remote_repo_test (master)
  $ git push
  Enumerating objects: 5, done.
  Counting objects: 100% (5/5), done.
  Delta compression using up to 4 threads
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 1.07 KiB | 546.00 KiB/s, done.
  Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
  remote: Resolving deltas: 100% (1/1), completed with 1 local object.
  To github.com:Pyrad/multi_remote_repo_test.git
     f6bff1b..124117d  master -> master
  Enumerating objects: 5, done.
  Counting objects: 100% (5/5), done.
  Delta compression using up to 4 threads
  Compressing objects: 100% (2/2), done.
  Writing objects: 100% (3/3), 1.07 KiB | 1.07 MiB/s, done.
  Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
  remote: Powered by GITEE.COM [GNK-6.3]
  To gitee.com:pyrad/multi_remote_repo_test.git
     f6bff1b..124117d  master -> master
  
  ```

  


# Reference

- [本地Git仓库关联多个远程仓库的两种方法](https://blog.csdn.net/s_156/article/details/120975674)
