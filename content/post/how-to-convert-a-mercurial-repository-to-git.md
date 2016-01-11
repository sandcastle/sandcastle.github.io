---
date: 2015-03-16
title: "How to convert a mercurial (hg) repository to git"
tags: [ "git", "hg" ]
categories: [ "development" ]
---

The easiest way to convert from `mercurial` (aka `hg`) to `git` is by using `hg-fast-export` on ubuntu. If you dont have ubnutu, then you can spin up a server on [Digital Ocean](https://digitalocean.com) for a few cents.

If you have issues with any of the below commands, try prefixing with `sudo` to elevate privileges.

## Install git & mercurial

First we need to install Git and Mercurial:

```
sudo apt-get install git mercurial -y
```

## Clone hg-fast-export

The `hg-fast-export` converter is run directly from its repo so we will need to clone it locally.

```bash
# we will convert our repos here
cd /tmp

# install converter
git clone https://github.com/frej/fast-export.git
```

## Clone your repository

To keep things simple we are just going to use HTTPS instead of SSH.

```shell
hg clone https://bitbucket.org/account/your-repo
```

For the above example this would result in a new folder being created called `/tmp/your-repo` - we will use this in the next next step.

## Export to git

Export your Mercurial repository to a new Git one

```shell
# create a new folder for the git version
mkdir your-repo-git
cd your-repo-git

# initialise the new git repository
git init

#run the export (don't forget to change your repo path below)
../fast-export/hg-fast-export.sh -r ../your-repo/
```

## Upload to git hosting

Finally, if you havent already done so, create a new git repo on your hosting provider and them push up the converted repository:

```shell
# set the address of your remote git repository
git remote add origin https://bitbucket.org/account/your-git-repo

# push up your changes
git push -u origin --all # pushes up the repo and its refs for the first time
git push -u origin --tags # pushes up any tags
```
