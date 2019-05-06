# Get ssl version on Mac OS High Serra

```console
$ ls -la /usr/lib | grep libssl
-rwxr-xr-x    1 root  wheel    392912 Jul  4  2018 libssl.0.9.7.dylib
-rwxr-xr-x    1 root  wheel    630144 Jul  4  2018 libssl.0.9.8.dylib
-rw-r--r--    1 root  wheel    947104 Mar 28 09:57 libssl.35.dylib
-rw-r--r--    1 root  wheel    890800 Mar 28 09:57 libssl.43.dylib
lrwxr-xr-x    1 root  wheel        15 Apr  6 19:08 libssl.dylib -> libssl.35.dylib

$ strings /usr/lib/libssl.0.9.8.dylib | grep "^OpenSSL \S\+ [0-9]\+ \S\+ [0-9]\+"
OpenSSL 0.9.8zh 14 Jan 2016
```

