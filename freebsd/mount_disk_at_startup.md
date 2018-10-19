# Mont disk at startup on Freebsd 11

```console
$ fsck -y
$ mount -u /
$ mount -a -t ufs
$ swapon -a
```
