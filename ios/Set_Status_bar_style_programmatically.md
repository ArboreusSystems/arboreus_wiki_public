# Set Status bar style globally programmatically

* Set in Info.plist:
```
<key>UIViewControllerBasedStatusBarAppearance</key>
<false/>
```
* Set in any Objective-C class:
```
[UIApplication sharedApplication].statusBarStyle = UIStatusBarStyleDarkContent;
[UIApplication sharedApplication].statusBarStyle = UIStatusBarStyleLightContent;
[UIApplication sharedApplication].statusBarStyle = UIStatusBarStyleDefault;
```
* Set in any Swift class:
```
// Will be working with warning "Setter for 'statusBarStyle' was deprecated in iOS 9.0: Use -[UIViewController preferredStatusBarStyle]"
UIApplication.shared.statusBarStyle = UIStatusBarStyle.lightContent;
```