# Arboreus Library module: a_time_now

The module for getting current time in different formats. Available like [Erlang NIF](http://erlang.org/doc/tutorial/nif.html) and console application. Written on C and Erlang. The sources available on [Github: Arboreus page](https://github.com/ArboreusSystems/arboreus_library).

## Install and compile

* Download or Clone Arboreus repository from [Gituhb](https://github.com/ArboreusSystems/arboreus_library)
* Use [make](https://en.wikipedia.org/wiki/Make_(software)) utility for installing and compiling 
```console 
$ /path/to/Arboreus/make install a_time
```

## Console application usage

* **./a_time_now microseconds** - return current time like UNIX-timestamp in microseconds
* **./a_time_now milliseconds** - return current time like UNIX-timestamp in milliseconds
* **./a_time_now seconds** - return current time like UNIX-timestamp in seconds
* **./a_time_now integer** - return current time like integer
* **./a_time_now integer_date** - return current date like integer
* **./a_time_now integer_full** - return current date and time like integer
* **./a_time_now integer_extend** - return current date and time within microseconds precise like integer
* **./a_time_now rfc_822** - return current date and time like RFC 822 string
* **./a_time_now rfc_850** - return current date and time like RFC 850 string
* **./a_time_now ansi** - return current date and time like ANSI string

```console
$ cd /path/to/Arboreus/bin/a_time
$ ./a_time_now microseconds
1547230925937008
$ ./a_time_now milliseconds
1547230943840
$ ./a_time_now seconds
1547230953
$ ./a_time_now integer
212239
$ ./a_time_now integer_date
20190111
$ ./a_time_now integer_full
20190111212250
$ ./a_time_now integer_extend
2019011121225670481
$ ./a_time_now rfc_822
Fri, 11 Jan 2019 21:23:06 GMT
$ ./a_time_now rfc_850
Friday, 11-Jan-19 21:23:10 GMT
$ ./a_time_now ansi
Fri Jan 11 21:23:15 2019
```

## Erlang NIF usage

Before make sure that a_time_now.so (NIF library object file) loaded into Erlang VM.

* **a_time_now:load_nif(Path_to_nif)** -> load object file
* **a_time_now:microseconds()** -> return current UNIX-timestamp   in microseconds like integer
* **a_time_now:milliseconds()** -> return current UNIX-timestamp   in milliseconds like integer
* **a_time_now:seconds()** -> return current UNIX-timestamp in seconds like integer
* **a_time_now:integer()** -> return current time like integer
* **a_time_now:integer_date()** -> return current date like integer
* **a_time_now:integer_full()** -> return current date and time like integer
* **a_time_now:integer_extend()** -> return current date and time within microseconds precise like integer
* **a_time_now:rfc_822()** -> return current date and time like RFC 822 string
* **a_time_now:rfc_850()** -> return current date and time like RFC 850 string
* **a_time_now:ansi()** -> return current date and time like ANSI string 

```console
Eshell V10.0  (abort with ^G)
(a_time@workstation.local)1> cd("/path/to/Arboreus/ebin/a_time").
/path/to/Arboreus/ebin/a_time
ok
(a_time@workstation.local)2> code:load_file(a_time_now).
{module,a_time_now}
(a_time@workstation.local)3> a_time_now:load_nif("/path/to/Arboreus/nif/a_time/a_time_now_nif").
ok
(a_time@workstation.local)4> a_time_now:microseconds().
1547231871121634
(a_time@workstation.local)5> a_time_now:milliseconds().
1547231878081
(a_time@workstation.local)6> a_time_now:seconds().
1547231885
(a_time@workstation.local)7> a_time_now:integer().
213811
(a_time@workstation.local)8> a_time_now:integer_date().
20190111
(a_time@workstation.local)9> a_time_now:integer_full().
20190111213854
(a_time@workstation.local)10> a_time_now:integer_extend().
2019011121390251301
(a_time@workstation.local)11> a_time_now:rfc_822().
"Fri, 11 Jan 2019 21:39:16 GMT"
(a_time@workstation.local)12> a_time_now:rfc_850().
"Friday, 11-Jan-19 21:39:23 GMT"
(a_time@workstation.local)13> a_time_now:ansi().
"Fri Jan 11 21:39:29 2019
```