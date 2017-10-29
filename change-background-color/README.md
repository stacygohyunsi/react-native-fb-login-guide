# Setup
Change the background color for react-native apps. 

To change the background color within the app, it is not possible to have a common setting to change all the `Views` etc. You can create a `StyleSheet` and apply it to multiple Views, headers etc.

# Changing the RootView color
Change the `RootView` color. `RootView` is a white flash just after the splash page of the app. 

![](https://3lhowb48prep40031529g5yj-wpengine.netdna-ssl.com/wp-content/uploads/2015/11/white-blip.gif)

## IOS

1. Edit `AppDelegate.m`. Find the line of code which says `rootView.backgroundColor` and change it to:

```
rootView.backgroundColor = [UIColor blackColor]; //if you want the color to be black
```
For other colors:
```
rootView.backgroundColor = [[UIColor alloc] initWithRed:.01f green:.75f blue:.54f alpha:1];
```

## Android

1. Go to `android/app/src/main/res/values/` in your app, and create (or edit) `colors.xml`
2. In `colors.xml`, add this code.
```
<resources>
  <color name="background">#AB47BC</color>
</resources>
```
3. In `styles.xml`, a theme customization item named `android:windowBackground`, referencing the chosen color name
```
<resources>
  <style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <item name="android:windowBackground">@color/background</item>
  </style>
</resources>
```

