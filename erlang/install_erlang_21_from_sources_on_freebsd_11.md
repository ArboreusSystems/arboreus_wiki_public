# Install Erlang 21 from sources on FreeBSD 11

### Install required packages 

```console
$ pkg install curl autoconf devel/gmake
```

### Download and extract sources

The src archive from official [download page](https://www.erlang.org/downloads) from Erlang site. If you need another version - visit this site.

```console
$ curl -o erlang_21.tar.gz http://erlang.org/download/otp_src_21.1.tar.gz
$ tar -xvf erlang_21.tar.gz
```

### Setup $ERL_TOP

Required by official [Installation manual](http://erlang.org/doc/installation_guide/INSTALL.html)

```console
$ cd otp_src_21.1
$ export ERL_TOP=`pwd`
```

### Setup Erlang 21 itself

```console
$ ./otp_build setup
```

### Add Erlang binary files to $PATH 

```console
$ export PATH=$PATH:`pwd`
```