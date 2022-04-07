---
title: Hexo git to different computer
date: 2021-07-19 17:03:06
categories:
- Hexo related
tags:
---


# Hexo git to different computer

<!-- more -->

## create a clean local hexo blog directory
install hexo first !
```shell
npm install hexo-cli -g
```

## Initialize hexo folder

```shell
# hexo init FOLDER_NAME
hexo init hexolocal
```

## Change "_config.yml"

```yaml
url: https://username.github.io/
...

deploy:
type: git
repo: https://github.com/username/username.github.io
branch: master
```

## Generate

```shell
# under hexo folder
hexo g

# view on the loclal
hexo s
```

## Pull the Blog page repo & copy the local hexo files to a different working branch

```shell
git clone git@github.com:Pyrad/Pyrad.github.io.git
cd Pyrad.github.io
git pull
```

## Create a new branch for hexo folder

```shell
# Create a new branch: hexo
git branch hexo
# Change to the new hexo branch for working !!!
git checkout hexo
```

## Clean the branch

```shell
git rm -rf .
```

## Copy all files inside the previous hexo folder here

```shell
cp -rf /path/to/hexolocal/.github .
cp -rf /path/to/hexolocal/scaffolds/ .
cp -rf /path/to/hexolocal/source/ .
cp -rf /path/to/hexolocal/themes/ .
cp -rf /path/to/hexolocal/.gitignore/ .
cp -rf /path/to/hexolocal/_config.*/ .
cp -rf /path/to/hexolocal/package.json/ .
cp -rf /path/to/hexolocal/package-lock.json/ .

git add .
git commit -m "create hexo branch for blog source files; Use this as the default working branch for blogging"
git push ### Should set up the upstream first
```

## Regenerate the hexo file modules

```shell
cnpm install
cnpm install hexo-deployer-git --save
```

## Try hexo

```shell
hexo -v
hexo g
hexo s
```

