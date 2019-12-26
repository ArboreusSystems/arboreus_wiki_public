# Do not show MacOS Catalina update notification

```console
$ killall "System Preferences"
$ sudo softwareupdate --ignore 'macOS Catalina'
$ defaults delete com.apple.systempreferences AttentionPrefBundleIDs
$ defaults delete com.apple.systempreferences DidShowPrefBundleIDs
$ rm ~/Library/Preferences/com.apple.preferences.softwareupdate.plist
$ killall Dock
```