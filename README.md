# Phabricator Quickstart

A template app to get [Phabricator](https://github.com/facebook/phabricator)
up and running on OpenShift.

# How To Use

## Requirements
* An OpenShift [account](https://openshift.redhat.com).
* 5-10 minutes of free time.

## Create the OpenShift Gear.

```shell
$ rhc-create-app -a phabricator -t php-5.3 -l [your username]
Password: 
Creating application: phabricator in [your namespace]
Now your new domain name is being propagated worldwide (this might take a minute)...
...
Successfully created application: phabricator
```

## Add the MySQL cartridge.

```shell
$ rhc-app cartridge add -c mysql-5.1 -a phabricator -l [your username]
Password: 

RESULT:

MySQL 5.1 database added.  Please make note of these credentials:
...
```

## Pull in this Quickstart repository.

```shell
$ cd phabricator
$ git remote add quickstart git://github.com/CodeBlock/phabricator-openshift-quickstart.git
$ git pull quickstart master
From git://github.com/CodeBlock/phabricator-openshift-quickstart
 * branch            master     -> FETCH_HEAD
Updating f1f79ce..303e532
...
```

## Move the config file in to place and customize it.

```shell
$ cp misc/myconfig.conf.php.dist misc/myconfig.conf.php
$ $EDITOR misc/myconfig.conf.php
```

Be sure to edit the domain name to point to your namespace/app.

## Push everything to openshift.

```shell
$ git push origin master
Counting objects: 16, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (9/9), done.
Writing objects: 100% (10/10), 2.13 KiB, done.
...
```

## Create an account for yourself

```shell
# Figure out what to ssh to.
$ grep rhcloud .git/config | sed 's/.*\/\(.\+\)\/~.*/\1/g'
[some random username]@phabricator-[your namespace].rhcloud.com

$ ssh [output from above]
```

Once you've ssh'd to the application, create a user using phabricator's `accountadmin`.

```shell
$ PHABRICATOR_ENV=custom/myconfig ./phabricator/repo/phabricator/bin/accountadmin
[follow the wizard to create a user]
```

## And finally...

Go to it in your browser:

https://phabricator-[your namespace].rhcloud.com/

Have fun!


# Thanks

Thank you to Evan Priestley for working with me in getting this working on OpenShift
and for the awesome job he's done (and continues to do) with developing Phabricator.
