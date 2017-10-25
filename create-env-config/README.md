# Setup
Adding different environments for react-native. We will be using `react-native-config` library in our project. 

## IOS

### Adding react-native-config to the project
1. yarn add react-native-config
2. react-native link react-native-config
3. Create `.env.dev`, `.env.staging`, and `.env.prod` files in the root of your project depending on the environments you want
4. Put in the variables for each environment in the files
4. Once it is done, you can access the variables via:
```
import Config from 'react-native-config'

Config.SERVER_URL;
Config.GOOGLE_API_KEY;
```

### Configuring XCode
3. In XCode, select your project, go to `Build Settings` > `Preprocess Info.plist` File
4. Set `Preprocess Info.plist` File to `Yes`
5. Set `Info.plist Preprocessor Prefix` File to `${BUILD_DIR}/GeneratedInfoPlistDotEnv.h`
6. Set `Info.plist Other Preprocessor Flags` to `-traditional`

### Duplicate schemes
7. In XCode go to Product > Scheme > Manage Schemes
8. Select your current scheme then select the gear icon, then "Duplicate"
8. Make sure that "Shared" is selected for your new schemes
9. Name your new scheme
10. Expand `Build` and click "Pre-actions"
11. Click the plus sign and then “New Run Script Action”
12. Paste this into the box (replacing `.env.dev` with the relevant file): 

```
echo ".env.dev" > /tmp/envfile
```