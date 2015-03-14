---
layout: post
category : cis
tags : [gerrit]
---

# Server Side

## Overview Scripts

```sh
cis=`pwd`
gerrit=$cis/gerrit
gerrit_ver=2.10

# download gerrit
# refer to: https://code.google.com/p/gerrit/
wget http://gerrit-releases.storage.googleapis.com/gerrit-$gerrit_ver.war

# install or upgrade gerrit
# it need do a lot of settings here. refer bellow.
# for upgrade, just press enter, then the previous settings are applied.
mkdir $gerrit
java -jar gerrit-$gerrit_ver.war init -d $gerrit

# start gerrit
cd $gerrit/bin
./gerrit.sh start
```

## Install Gerrit Detailed Instructions

Here is an example to setup with LDAP authentication.

```sh
~/cis$ java -jar gerrit-2.10.war init -d gerrit

*** Gerrit Code Review 2.10
***


*** Git Repositories
***

Location of Git repositories   [git]:

*** SQL Database
***

Database server type           [h2]:

*** Index
***

Type                           [LUCENE/?]:

The index must be rebuilt before starting Gerrit:
  java -jar gerrit.war reindex -d site_path

*** User Authentication
***

Authentication method          [LDAP/?]:
LDAP server                    [ldap://ldap.company.com]:
LDAP username                  [user@company.com]:
Change user@company.com's password [y/N]?
Account BaseDN                 [OU=Workers,dc=company,dc=com]:
Group BaseDN                   [OU=Workers,dc=company,dc=com]:

*** Review Labels
***

Install Verified label         [y/N]? y

*** Email Delivery
***

SMTP server hostname           [localhost]:
SMTP server port               [(default)]:
SMTP encryption                [NONE/?]:
SMTP username                  :

*** Container Process
***

Run as                         [yourname]:
Java runtime                   [/usr/lib/jvm/java-7-openjdk-amd64/jre]:
Upgrade /home/yourname/cis/gerrit/bin/gerrit.war [Y/n]?
Copying gerrit-2.10.war to /home/yourname/cis/gerrit/bin/gerrit.war

*** SSH Daemon
***

Listen on address              [*]:
Listen on port                 [29418]:

*** HTTP Daemon
***

Behind reverse proxy           [y/N]?
Use SSL (https://)             [y/N]?
Listen on address              [*]:
Listen on port                 [8080]:
Canonical URL                  [http://10.99.116.110:8080/]:

*** Plugins
***

Install plugin commit-message-length-validator version v2.10 [y/N]? y
Install plugin download-commands version v2.10 [y/N]? y
Install plugin replication version v2.10 [y/N]? y
Install plugin reviewnotes version v2.10 [y/N]? y
Install plugin singleusergroup version v2.10 [y/N]? y
version v2.9.4 is already installed, overwrite it [y/N]? y

Initialized /home/chenys/cis/gerrit
~/cis$ cd gerrit/bin
~/cis/gerrit/bin$ ls
gerrit.sh  gerrit.war
~/cis/gerrit/bin$ ./gerrit.sh start
Starting Gerrit Code Review: OK
```

Note: for "Install Verified label         [y/N]?", if you or jenkins need label Verified, then please set it as y.

## Setup user accounts

1. open http://10.99.116.110:8080
2. login with your username (say yourname), the first login user is the administrator (ID=1).
3. for other uses, can login after you have login.

## Setup access permissions

### Setup access permissions for All-Projects

Make necessary changes for default configurations, say support wip branch.

```
Reference:	refs/heads/wip/*
  Create Reference
    Registered Users
  Push Exclusive
    Registered Users       Force Push
```

### Setup access permissions for other projects

1. inherite from All-Projects
2. add project specified permissions

## Create projects (repositories) in server

in [Projects] >> [Create New Project], set bellow

```
Project Name:           <name of the project>
Rights Inherit From:		<suggest to be All-Projects>
Create initial empty commit
Only serve as parent for other projects
```

in [Projects] >> [General], set bellow

```
Submit Type:            Cherry Pick
```

## Setup jenkins user for jenkins

1. In the shell, run bellow:

  ```sh
  ssh -p 29418 yourname@localhost gerrit create-account jenkins --ssh-key - < ~/.ssh/id_dsa.pub
          or
  ssh -p 29418 yourname@10.99.116.110 gerrit create-account jenkins --ssh-key - < ~/.ssh/id_dsa.pub
  ```
2. Open gerrit web (http://10.99.116.110:8080), in [Projects] > [All-Projects] > [Access], set

  ```
  Global Capabilities	
    Administrate Server
      ALLOW Administrators
    Priority
      Non-Interactive Users
    Stream Events
      Non-Interactive Users
  
  Reference:	refs/heads/*
    Label Code-Review Exclusive
      -1 +1  user/Jenkins (jenkins)
    Label Verified Exclusive
      -1 +1  user/Jenkins (jenkins)
  ```
3. Add jenkins to group "Non-Interactive Users".

   Do it in [People] > [Non-Interactive Users] > [Members], click Add.

# Client Side

## Register Users

1. Login gerrit web with your Windows (LDAP) user name and password.
2. Add you local public key to gerrit.
   * in top-right, click your user name, then [Settings] > [SSH Public Keys] > [Add Key..]
   * Get key with bellow command.

      ```sh
      $ cat ~/.ssh/id_dsa.pub
      ```
   * If you can't find the key, then use bellow command to generate one.

      ```sh
      $ ssh-keygen
      ```
3. Change other necessary settings in [Settings] > [Profile], say User Name
