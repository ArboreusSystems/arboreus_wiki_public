# Building libzip library for iOS on MacOS High Sierra

Libzip version: 1.5.1, Target OS: MacOS High Sierra

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
* Create build directory
```console
$ cd [path/to/libzip/directory]
$ mkdir build
```
* Run CMake in the build directory, it will configure library 
```console
$ cmake ..
```
* Add the preferred architecture and iPhoneOS.sdk location in [path/to/libzip/directory]/build/CMakeFiles/zip.dir/flags.make (do not care about notice "DO NOT EDIT!" In this file, just do it):
```make
# -----------------------
# Write this:

C_FLAGS += -arch arm64
C_FLAGS += -isysroot [path/to/iPhoneOS.sdk]
# By default it looks like 
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk just check it
C_FLAGS += -fPIC -fvisibility=hidden

# -----------------------
# In exchange of this:

C_FLAGS = -fPIC -fvisibility=hidden
```
* Do installation process in [path/to/libzip/directory]/build
```console
$ cd [path/to/libzip/directory]/build
$ make
```
* Go to the directory where compiled object files (*.o) [path/to/libzip/directory]/build/CMakeFiles/zip.dir/ (it's the same where located flags.make) and run the "ar" command:
```console
$ ar -rv libzip_arm64.a *.o
```

If you need another architecture just follow this guidance but change the type of architecture. If you going to use it in Qt do not [disable BITCODE for iOS application](https://forum.qt.io/topic/69409/disable-bitcode-for-ios-project/6)