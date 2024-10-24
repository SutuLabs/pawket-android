# Put artifact at www folder
```
mkdir www
cp -rp artifact www/
```
# Install Cordova

```
npm install -g cordova
cordova platform add android
```

# Install Android Development Tools

## Java Development Kit (JDK)

```
brew tap adoptopenjdk/openjdk
brew install --cask adoptopenjdk8
```

## Gradle

```
brew install gradle
```

## Android SDK

1. Install [Android Studio](https://developer.android.com/studio/index.html)
2. Adding SDK Packages

    Open the Android SDK Manager (Tools > SDK Manager in Android Studio, or sdkmanager on the command line), and make sure the following are installed:

   - Android Platform SDK for your targeted version of Android

   - Android SDK build-tools version 29.0.2 or higher

    Open the Android Studio SDK Manager

    1. In the Android SDK Tools tab, uncheck Hide Obsolete Packages
    
    2. Check Android SDK Tools (Obsolete)

## Setting environment variables
1. Set the JAVA_HOME environment variable to the location of your JDK installation
2. Set the ANDROID_SDK_ROOT environment variable to the location of your Android SDK installation
3. It is also recommended that you add the Android SDK's tools, emulator and platform-tools directories to your PATH

```sh
export JAVA_HOME=<java-location>
export ANDROID_SDK_ROOT=<sdk-location>
export ANDROID_HOME=<sdk-location>
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools/
export PATH=$PATH:$ANDROID_SDK_ROOT/tools/
export PATH=$PATH:$ANDROID_SDK_ROOT/emulator/
```


```sh
export ANDROID_SDK_ROOT=/c/Users/icer/AppData/Local/Android/Sdk
export ANDROID_HOME=/c/Users/icer/AppData/Local/Android/Sdk
```

# Check
In the cordova project directory, run
```
cordova requirements
```
If you have successfully installed all the required tools above, the result should be like:
```
Requirements check results for android:
Java JDK: installed 1.8.0
Android SDK: installed true
Android target: installed android-32,android-30,android-29
Gradle: installed /usr/local/Cellar/gradle/7.4/bin/gradle
```

# Build
```
cordova build
```
# Test in Emulator
1. Create a Device

    Android Studio - Virturl Device Manager - Create Device
2. Run App
```
cordova run android --emulator
```

# Release

1. Modify version in `config.xml`.
2. Replace files in `www\` with latest package download from [Azure Devops Pipelines](https://dev.azure.com/sututech/Chia/_build?definitionId=43&_a=summary).
3. Build release with `yarn build:release`.
4. Upload aab package to [Google Play Console](https://play.google.com/console/u/0/developers/6182797017495156447/app/4973812058919766560/tracks/production)
  - Production -> Create Release -> Upload
5. Download `Signed, universal APK` from app bundle.
6. Remember to upload latest APK to github release.

# Upgrade API version

`config.xml`
```xml
    <preference name="android-targetSdkVersion" value="35" />
```

```sh
cordova platform remove android
cordova platform add android
sdkmanager.bat "platforms;android-35"
sdkmanager.bat "build-tools;35.0.0"
cordova requirements
yarn build:release
```

# FAQ

**Q:** How do I fix the “Unsupported class file major version 66” error when compiling Android with Cordova?

**A:** This is caused by using a Java version that's too high; downgrading to Java 17 will resolve the issue.