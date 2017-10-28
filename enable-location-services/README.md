# Setup
Getting the user's location 

## IOS

1. Include the `NSLocationWhenInUseUsageDescription` key in `Info.plist` to enable geolocation
2. Add location as a background mode in the `Capabilities` tab in XCode
3. To simulate a location on simulator, go to Debug > Simulate Location

## Android

Add the following line of code to `AndroidManifest.xml`
```
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

