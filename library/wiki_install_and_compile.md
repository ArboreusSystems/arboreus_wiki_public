# Install and compile Arboreus Library.

* make sure that you have installed Clang compiler and Erlang compiler. If not - install it before.
* Download or Clone Arboreus repository from [Github](https://github.com/ArboreusSystems/arboreus_library)
* create in /path/to/Arboreus/make directory from file directories.tmpl.mk the file directories.conf.mk and ad to this file path to the Erlang headers files directory. Usually it looks like /path/to/Erlang/erts-10.0/include/
```console
$ cd /path/to/Arboreus/make
$ cp directories.tmpl.mk directories.conf.mk
$ nano directories.conf.mk

H_DIRECTORIES = \
	-I/path/to/Erlang/21.0/erts-10.0/include/
```
* Use [make](https://en.wikipedia.org/wiki/Make_(software)) utility for installing and compiling 
```console 
$ /path/to/Arboreus/make install a_time
```
