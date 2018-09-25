# Install Wiki.js and Apache SSL on FreeBSD 11

## Prerequisites 

This application might be very useful and cheap solution for organising companies Wiki pages based on  [Markdown](https://www.markdownguide.org)

* You have already installed FreeBSD 11
* All of this manual based on official documentation for Linux and MacOS
* Download Wiki.js sources from [official repository](https://github.com/Requarks/wiki/releases/)

## Installation 

```console
$ pkg install mongodb34 git node www/npm
$ mkdir /path/to/custom/wiki /path/to/custom/mongodb
$ nano /usr/local/etc/mongodb.conf

- change default directory
- change mongo bind IP

$ nano /etc/rc.conf

# MongoDD
mongod_enable="YES"

$ chown -R mongodb:mongodb /path/to/custom/mongodb/
$ cd /path/to/custom/wiki
$ curl -L -s -S https://github.com/Requarks/wiki/releases/download/v1.0.102/node_modules.tar.gz >> node_modules.tar.gz
$ tar xzf - < node_modules.tar.gz
$ curl -L -s -S https://github.com/Requarks/wiki/releases/download/v1.0.102/wiki-js.tar.gz >> wiki-js.tar.gz
$ tar xzf - < wiki-js.tar.gz
$ rm node_modules.tar.gz wiki-js.tar.gz
$ cp -n config.sample.yml config.yml
$ nano config.yml

- setup MongoDB IP

$ node wiki configure

- setup it via browser, follow application instructions
```

If you need SSL you might to use Apache proxy functionality and use Wiki.js behind it.