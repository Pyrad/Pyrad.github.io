---
title: Create my first blog on Github
date: 2021-07-19 20:42:38
categories:
- Hexo related
tags:
---

## How to create my first blog on Github

1. First install nodejs

2. Install 'cnpm' because of "Great Fire Wall"
   
   ```bash
   npm install -g cnpm --registry=https://registry.npm.taobao.org
   ```
   
3. Install hexo

   ```bash
   cnpm install -g hexo-cli
   ```

4. Check if hexo is installed: 

   ```bash
   hexo -v
   ```

   

4. cd a new blog directory, then 
   
   ```bash
   mkdir -p /path/to/blogdir
   cd /path/to/blogdir
   hexo init
   ```
   
   
   
6. Start hexo service

   ```bash
   hexo s
   ```

   This would print the following messages, and we could check it locally with http://localhost:4000

   ```bash
   INFO  Validating config
   INFO  Start processing
   INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
   ```

   

7. Create another blog file: hexo n "NewFileName"

   ```bash
   hexo n <TheNewFileName>
   ```

   

   You could see the new file is created: **/path/to/blogdir/source/_post/TheNewFileName**
   You could edit it as you want

8. After editing is done, go back to /path/to/blogdir, use command to clean

   ```java
   hexo clean
   ```

   

9. Generate:

   ```java
   hexo g
   ```

   Now you could see you blog file by starting the local service again

   ```bash
   hexo s
   ```

   check at: http://localhost:4000

10. Next steps are to deploy your blog to your Github repository

11. First create you own page by create a new Github repo as: **Pyrad.github.io**
    Here 'Pyrad' is the nickname of my account, and it must be in such name format

12. Go back to **/path/to/blogdir**, use the command below to install a plugin

    ```bash
    > cnpm install --save hexo-deployer-git
    D:\MyBlog> cnpm install --save hexo-deployer-git
    | [0/1] Installing domhandler@^4.2.0platform unsupported hexo-deployer-git@3.0.0 › hexo-fs@3.1.0 › chokidar@3.5.2 › fsevents@~2.3.2 Package require os(darwin) not compatible with your platform(win32)
    [fsevents@~2.3.2] optional install error: Package require os(darwin) not compatible with your platform(win32)
    √ Installed 1 packages
    √ Linked 53 latest versions
    √ Run 0 scripts
    √ All packages installed (53 packages installed from npm registry, used 7s(network 7s), speed 396.44KB/s, json 53(143.2KB), tarball 2.56MB)
    ```

13. Edit *_config.yml*

    ```shell
    D:\MyBlog>dir
     Volume in drive D is 本地磁盘
     Volume Serial Number is 40E8-0C16
    
     Directory of D:\MyBlog
    
    2021/07/18  10:11    <DIR>          .
    2021/07/18  10:11    <DIR>          ..
    2021/07/18  09:56    <DIR>          .github
    2021/07/18  09:56                71 .gitignore
    2021/07/18  10:22            31,683 db.json
    2021/07/18  10:27    <DIR>          node_modules
    2021/07/18  09:57            56,333 package-lock.json
    2021/07/18  10:27               655 package.json
    2021/07/18  10:11    <DIR>          public
    2021/07/18  09:56    <DIR>          scaffolds
    2021/07/18  09:56    <DIR>          source
    2021/07/18  09:56    <DIR>          themes
    2021/07/18  09:56                 0 _config.landscape.yml
    2021/07/18  09:56             2,546 _config.yml
                   6 File(s)         91,288 bytes
                   8 Dir(s)  29,096,636,416 bytes free
    ```

    change the Deployment section as below:

    ```yaml
    # Deployment
    ## Docs: https://hexo.io/docs/one-command-deployment
    deploy:
      type: git
      repo: git@github.com:Pyrad/Pyrad.github.io.git
      branch: master
    ```

    Here *repo* is the ssh address for my github page

14. Using hexo to deploy (didn't succeed, to handle with SSH key)

    ```shell
    hexo d
    ```

    Note that it would be better using Git bash here.

    ```shell
    Pyrad@SSEA MINGW64 /d/MyBlog
    $ hexo d
    INFO  Validating config
    INFO  Deploying: git
    INFO  Clearing .deploy_git folder...
    INFO  Copying files from public folder...
    INFO  Copying files from extend dirs...
    warning: LF will be replaced by CRLF in 2021/07/18/My-first-blog-file/index.html.
    The file will have its original line endings in your working directory.
    ... ...
    warning: LF will be replaced by CRLF in js/script.js.
    The file will have its original line endings in your working directory.
    On branch master
    nothing to commit, working tree clean
    Permission denied (publickey).
    fatal: Could not read from remote repository.
    
    Please make sure you have the correct access rights
    
    ```

    Here an error happened, because the RSA key has not been created yet, or it has been created  while it has a different name.

    In general, the following command will be used to created the key

    ```shel
    # Create a SSH key, it will create 'id_rsa.pub' in ~/.ssh
    ssh-keygen -t rsa
    ```

    But sometimes you'd like to use a different name other than the default name, then you add an option

    ```shell
    ssh-keygen -t rsa -C "YouEmail@example.com"
    ```

    then a key file with different name is created, as below,

    ```shell
    Pyrad@SSEA MINGW64 /d/MyBlog
    $ ls ~/.ssh/
    github_rsa  github_rsa.pub  known_hosts
    ```

    In this circumstances, when you type the following command, it reports errors

    ```shell
    Pyrad@SSEA MINGW64 /d/MyBlog
    $ ssh -T git@github.com
    Permission denied (publickey).
    ```

    That is because it uses the default name ***id_rsa*** to try the connection, while you only have ```github_rsa``` which is a non-default name, so create a default key file, or add a config file (```~/.ssh/config```) as below to specify your own key file

    ```shell
    Host github.com
     HostName github.com
     User Pyrad
     IdentityFile ~/.ssh/github_rsa
    ```

15. Deploy again (succeeded)

    ```shell
    hexo d
    ```

    It succeeded this time,

    ```shell
    Pyrad@SSEA MINGW64 /d/MyBlog
    $ hexo d
    INFO  Validating config
    INFO  Deploying: git
    INFO  Clearing .deploy_git folder...
    INFO  Copying files from public folder...
    INFO  Copying files from extend dirs...
    On branch master
    nothing to commit, working tree clean
    Counting objects: 46, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (34/34), done.
    Writing objects: 100% (46/46), 885.75 KiB | 2.61 MiB/s, done.
    Total 46 (delta 7), reused 0 (delta 0)
    remote: Resolving deltas: 100% (7/7), done.
    To github.com:Pyrad/Pyrad.github.io.git
     + 90d1898...2c43a78 HEAD -> master (forced update)
    Branch master set up to track remote branch master from git@github.com:Pyrad/Pyrad.github.io.git.
    INFO  Deploy done: git
    ```

16. Now you could view your page by visiting [Pyrad's Blog Page](https://pyrad.github.io/)

17. If you change your blog files later or add a new file, you could push the changes again by the following commands

    ```shell
    hexo clean
    hexo g #If a different theme is applied or other operations is done
    hexo s #Just for local preview
    hexo d
    ```

    

## References

- Bilibili video [Code Sheep's tutorial](https://www.bilibili.com/video/BV1Yb411a7ty?t=1686)
