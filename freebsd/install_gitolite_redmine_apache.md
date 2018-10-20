# Install Gitolite, Redmine, Apache on FreeBSD 11.

This installation guide done in the jail operated by Ezjail on Freebsd.  

### Install Gitolite

On Server:
```console
$ cd /usr/ports/devel/git && make install clean
$ cd /usr/ports/devel/gitolite && make install clean (Add git user in properties)
$ chsh -s /usr/local/bin/bash git
$ chmod g-w /projects/git/
$ mkdir /projects/git && chown git:git /projects/git
$ pw usermod git -d /projects/git
```

2. Install MySQL
3. Install Apache
4. Install Ruby, Ruby-Gems, Ruby-Iconv
5. [Generate SSL](https://github.com/ArboreusSystems/arboreus_wiki_public/blob/master/freebsd/self_signed_ssl_certificate_creating.md)
6. Install Redmine
7. Fix Redmine + Git "no-color" problem
8. Setting Redmine up