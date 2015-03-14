---
layout: post
category : cis
tags : [gerrit]
---

# Overview Scripts

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

# Install Gerrit Detailed Instructions

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

Run as                         [devenv]:
Java runtime                   [/usr/lib/jvm/java-7-openjdk-amd64/jre]:
Upgrade /home/devenv/cis/gerrit/bin/gerrit.war [Y/n]?
Copying gerrit-2.10.war to /home/devenv/cis/gerrit/bin/gerrit.war

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
