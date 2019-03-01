# Building libzip library on MacOS High Sierra

Libzip version: 1.5.1
Target OS: MacOS High Sierra
Installed dependency:

* OpenSSL: /usr/lib/libcrypto.dylib (found version "1.0.2o")
* ZLIB: /usr/lib/libz.dylib (found version "1.2.11")
* BZip2: /usr/lib/libbz2.dylib (found version "1.0.6")

For building shared/static [libzip](https://libzip.org) you need:

* To be installed all libraries that required above
```console
$ brew install zlib
$ brew install ...
```
* Make sure that you have [CMake](https://cmake.org) installed and working perfectly
* Download sources from [libzip.org](https://libzip.org/download/) or repository on [Github](https://github.com/nih-at/libzip/)
* If you need to make libzib like static library (*.a) add this lines to end of [path/to/libzip/directory]/lib/CMakeLists.txt
```cmake
ADD_LIBRARY(zipstatic STATIC 
	${LIBZIP_SOURCES}
	${LIBZIP_EXTRA_FILES}
	${LIBZIP_OPTIONAL_FILES}
	${LIBZIP_OPSYS_FILES}
	)
```
* Create build directory
```console
$ cd [path/to/libzip/directory]
$ mkdir build
```
* Run CMake in the build directory
```console
$ cmake ..
```
* Do installation process
```console
$ make
$ make test
$ make install
```