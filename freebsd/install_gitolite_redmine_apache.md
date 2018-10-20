# Install Gitolite, Redmine, Apache on FreeBSD 11.

This installation guide done in the jail operated by Ezjail on Freebsd 11.  

#### 1. Install Gitolite

On Server:
```console
$ cd /usr/ports/devel/git && make install clean
$ cd /usr/ports/devel/gitolite && make install clean 

# NOTICE!
# Add the user at time of configuring Gitolite

$ chsh -s /usr/local/bin/bash git
$ chmod g-w /path/to/git/
$ mkdir /path/to/git && chown git:git /path/to/git
$ pw usermod git -d /path/to/git
```
On Client:
```console
# Copy the user SSH key.pub to /tmp on server
```

2. Install MySQL
3. Install Apache
4. Install Ruby, Ruby-Gems, Ruby-Iconv
5. [Generate SSL](https://github.com/ArboreusSystems/arboreus_wiki_public/blob/master/freebsd/self_signed_ssl_certificate_creating.md)
6. Install Redmine
7. Fix Redmine + Git "no-color" problem
8. Setting Redmine up