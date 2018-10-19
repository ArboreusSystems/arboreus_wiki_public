# Getting users and groups lists on FreeBSD 11.

* Users list 
```console
$ awk -F":" '{print $1}' /etc/passwd 
```
* Groups list
```console
$ awk -F":" '{print $1}' /etc/group
```

