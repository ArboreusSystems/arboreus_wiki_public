# Build QtCipherSqlitePlugin on MacOS.

Based on:

* [Plugin sources](https://github.com/devbean/QtCipherSqlitePlugin)
* [Plugin Wiki](https://github.com/devbean/QtCipherSqlitePlugin/wiki)

The build environment:

* Qt 5.12.2
* MacOS High Sierra 

For building this plugin you need:

* Clone plugin from Github
```console
$ git clone https://github.com/devbean/QtCipherSqlitePlugin.git
```
* Open QtCipherSqlitePlugin.pro in Qt Creator
* Build it in Qt Creator
* Copy everything from [build_directory]/sqlitecipher/plugins/sqldrivers to [QT_HOME]/5.12.2/clang_64/plugins/sqldrivers
* Restart Qt Creator

The plugin usage described over [here](https://github.com/devbean/QtCipherSqlitePlugin/wiki/How-to-use). For setting up the encryption type use setConnectOptions("CONNECT_OPTION"). The  source part where handling located in [sqlitecipher.cpp](https://github.com/devbean/QtCipherSqlitePlugin/blob/master/sqlitecipher/sqlitecipher.cpp). Follow row 855 and below. Beside all of it follow this instruction [Guide for 1.x](https://github.com/devbean/QtCipherSqlitePlugin/wiki/Guide-for-1.x#set-default-cipher)

For building it for iOS follow [instructions](https://github.com/devbean/QtCipherSqlitePlugin/wiki/Plugin-for-iOS)

Follow published [example](https://github.com/ArboreusSystems/arboreus_examples/tree/master/qt/UsingQtCipherSqlitePlugin)
