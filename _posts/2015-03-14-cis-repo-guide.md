---
layout: post
category : cis
tags : [gerrit]
---

# Server Side Setup

## Clone git-repo.git from Google to Native Server

```sh
# download repo git to speed up initialization
git clone --mirror https://gerrit.googlesource.com/git-repo.git $gerrit/git/git-repo.git
```

## Configure default.xml in manifests.git

it's for the configurations of repo.
see https://gerrit.googlesource.com/git-repo/+/master/docs/manifest-format.txt for more details.

default.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
        <remote name="origin"
                fetch="."
                review="http://10.37.116.110:8080" />
        <default revision="master"
                remote="origin"
                sync-j="8" />
        <project path="app/calc" name="calc" />
        <project path="app/test" name="test" />
</manifest>
```

# Client Side

## Install repo application

```sh
install_repo()
{
        # get repo application for client side
        sudo curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > /usr/local/bin/repo
        sudo chmod a+x /usr/local/bin/repo
}
```

## Fetch the code from server by repo

```sh
server="10.37.116.110"
repos=`pwd`/repos

# setup git configuration if necessary
gitconfig()
{
        # global configurations for current user, in ~/.gitconfig
        git config --global user.name "Yongsen Chen"
        git config --global user.email yongsenchen@google.com
        git config --global core.fileMode false

        # operations alias for all users, in /etc/gitconfig
        sudo git config --system alias.st status
        sudo git config --system alias.ci commit
        sudo git config --system alias.co checkout
        sudo git config --system alias.br branch
        sudo git config --system alias.sh show
}

# fetch code
fetch_code()
{
        mkdir -p $repos
        cd $repos
        # note: when fetch code, must use ssh://$server:29418, http can't work
        repo init -u ssh://$server:29418/manifests -b master --repo-url=ssh://$server:29418/git-repo.git
        repo sync
        repo forall -c "scp -p -P 29418 $server:hooks/commit-msg .git/hooks/"
}
```
