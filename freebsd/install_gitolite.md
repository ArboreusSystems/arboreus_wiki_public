# Install Gitolite on Freebsd 11

## Prerequisites

* You have already installed FreeBSD 11
* You might need to define separated partition for the home directory of the user where you going to store repositories because of security polices (if you'll have it)
* Define special user for Gitolite actions (might be used configuration dialog at time of installation Gitolite)
* All access to repositories via SSH, the SSH client and server have to be installed before
* All of this example based on official [manual from Gitolite](http://gitolite.com/gitolite/install/)

## Installation

* On server
```console
$ cd /usr/ports/devel/git && make install clean
$ cd /usr/ports/devel/gitolite && make install clean (Add git user in properties)
$ chsh -s /usr/local/bin/bash git
$ mkdir /path/to/user/home/directory && chown git:git /path/to/user/home/directory
$ pw usermod git -d /path/to/user/home/directory
$ chmod g-w /path/to/user/home/directory
```
* On client: copy key.pub to the /tmp directory on server
* On server
```console
$ su - git
$ gitolite setup -pk /tmp/key.pub
$ exit
```
* On client
```console
$ git clone git@server.name:gitolite-admin.git
```