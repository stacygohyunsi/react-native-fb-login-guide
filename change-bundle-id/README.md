# Setup
Changing the BundleID because react-native defaults to org.react-native.example.xxx

## IOS
In Project > Target > Info, change the bundle Identifier key while still including `.$(PRODUCT_NAME:rfc1034identifier)` in the bundle Identifier. You may change the Bundle Name as well. Do not change it in `info.plist` in your project as info.plist pulls from the info section in XCode. 