# Install Gitolite, Redmine, Apache on FreeBSD 11.

This installation guide done in the jail operated by Ezjail on Freebsd 11 equipped Nano text editor. The installation process done under the root.

The applications manifest:
* Gitolite: gitolite-3.6.8,1
* Apache: apache-2.4.35
* MySQl: mysql56-server-5.6.41_2
* Redmine: redmine-3.4.6

#### 1. Install Gitolite

On Server:
```console
$ cd /usr/ports/devel/git && make install clean
$ cd /usr/ports/devel/gitolite && make install clean 

>>> NOTICE!
>>> Add the user at time of configuring Gitolite

$ chsh -s /usr/local/bin/bash git
$ chmod g-w /path/to/git/
$ mkdir /path/to/git && chown git:git /path/to/git
$ pw usermod git -d /path/to/git
```
On Client:
```console
>>> NOTICE!
>>> Copy the user SSH key.pub to /tmp on server
```
On Server:
```console
$ su - git
$ gitolite setup -pk /tmp/kirilov.pub
$ cd ~
$ exit
$ nano /path/to/git/.gitolite.rc

>>> NOTICE!
>>> Change the permition for repository folders in the .gitolite.rc

>>> UMASK                           =>  0027,

$ exit
```

#### 2. Install MySQL

```console
$ cd /usr/ports/databases/mysql55-server/ && make BATCH=yes install clean
$ nano /etc/rc.conf

>>> NOTICE!
>>> Add to rc.conf 
>>> # MySQL Daemon
>>> mysql_enable="YES"

$ chsh -s /usr/local/bin/bash mysql
$ mkdir /path/to/mysql/db/folder /path/to/mysql/db/folder/tmp /path/to/mysql/db/folder/secure 
$ pw usermod mysql -d /path/to/mysql/db/folder
$ chown -R mysql:mysql /path/to/mysql/db/folder
$ service mysql-server start
$ mysql_secure_installation

>>> NOTICE!
>>> Do the improving of security 

$ mysql -u root -p

>>> > UPDATE mysql.user set user = 'your_user_name' where user = 'root';
>>> > flush privileges;
>>> > CREATE DATABASE redmine;
>>> > CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'password';
>>> > GRANT ALL ON redmine.* TO 'redmine'@'localhost';
>>> > exit

$ mysql -u your_user_name -p

>>> > exit

$ mysql -u redmine -p

>>> > SHOW DATABASES;
>>> > exit
```


3. Install Apache
4. Install Ruby, Ruby-Gems, Ruby-Iconv
5. [Generate SSL](https://github.com/ArboreusSystems/arboreus_wiki_public/blob/master/freebsd/self_signed_ssl_certificate_creating.md)
6. Install Redmine
7. Fix Redmine + Git "no-color" problem
8. Setting Redmine up