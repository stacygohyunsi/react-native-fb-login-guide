# Setup
Adding a facebook login for react-native

## Android
My react-native version is 0.29. 

### MainApplication.java
In `MainApplication.java`, add the following code to it.

```
import com.facebook.CallbackManager;
import com.facebook.FacebookSdk;
import com.facebook.reactnative.androidsdk.FBSDKPackage;
import com.facebook.appevents.AppEventsLogger;
...
public class MainApplication extends Application implements ReactApplication {

  private static CallbackManager mCallbackManager = CallbackManager.Factory.create();

  protected static CallbackManager getCallbackManager() {
    return mCallbackManager;
  }
```
```
@Override
public void onCreate() {
  super.onCreate();
  FacebookSdk.sdkInitialize(getApplicationContext());
  // If you want to use AppEventsLogger to log events.
  AppEventsLogger.activateApp(this);
}
```

Register sdk package in method `getPackages()`.
```
private final ReactNativeHost mReactNativeHost = new ReactNativeHost(this) {
    @Override
    public boolean getUseDeveloperSupport() {
      return BuildConfig.DEBUG;
    }

    @Override
    protected List<ReactPackage> getPackages() {
      return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new FBSDKPackage(mCallbackManager)
      );
    }
};
```

### MainActivity.java
Override `onActivityResult()` method
```
import android.content.Intent;

public class MainActivity extends ReactActivity {

    @Override
    public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        MainApplication.getCallbackManager().onActivityResult(requestCode, resultCode, data);
    }
    //...
```

### build.gradle
In `android > build.gradle`, add `mavenCentral()` to `buildscript { repositories {}}`.

In `android > app > build.gradle`, add `compile 'com.facebook.android:facebook-android-sdk:[4,5)'` to `dependencies {}`.

### strings.xml
In `strings.xml`, add a new string with the name facebook_app_id and value as your Facebook App ID.
```
<string name="facebook_app_id">546333345453755</string>    
```

### AndroidManifest.xml
Add a uses-permission element to the manifest
```
<uses-permission android:name="android.permission.INTERNET"/>
```

```
<application android:label="@string/app_name" ...>
    ...
    <meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
    ...
</application>
```

## IOS
1. yarn add react-native-fbsdk
2. react-native link

### Configure Facebook App Settings
3. Select your Facebook App, Settings > Add Platform > IOS
4. Add the Bundle Identifier Xcode to Bundle ID
5. Enable Single Sign On

### Download Facebook SDK for iOS
6. Download Facebook SDK for iOS - name it **FacebookSDK** folder.
7. Open your Xcode, create a Frameworks group in your project
8. Drag **Bolts.framework, FBSDKCoreKit.framework, FBSDKLoginKit.framework, and FBSDKShareKit.framework** files into the Frameworks group
9. choose **Create groups** for any added folders and **deselect Copy items** if needed.
10. Go to Project > Build Settings > All > Framework Search Paths > Copy the path of your **FacebookSDK** folder and paste it there

### Configure info.plist folder

11. Add the following info to your info.plist inside the IOS folder > projectName (to make it easier, go to quick start and copy the prefilled information)

```
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>fb{your-app-id}</string>
			</array>
		</dict>
	</array>
	<key>FacebookAppID</key>
	<string>{your-app-id}</string>
	<key>FacebookDisplayName</key>
	<string>{your-app-name}</string>
```

### Connect App Delegate
Add the following to your AppDelegate.m file. 

```
#import <FBSDKCoreKit/FBSDKCoreKit.h>

- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {
    return [[FBSDKApplicationDelegate sharedInstance] application:application
                                                          openURL:url
                                                sourceApplication:sourceApplication
                                                       annotation:annotation];
}

- (void)applicationDidBecomeActive:(UIApplication *)application {
  [FBSDKAppEvents activateApp];
}
```

12. Add Facebook Login as a product in your Facebook app dashboard