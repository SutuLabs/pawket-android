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
4. Upload aab package to [Google Play Console](https://play.google.com/console/u/0/developers/4723266972324399816/app/4972761195466309737/tracks/4701725921608018730/releases/1/prepare)
5. Download `Signed, universal APK` from app bundle.

# Upgrade API version

`config.xml`
```xml
    <preference name="android-targetSdkVersion" value="33" />
```

```sh
cordova platform remove android
cordova platform add android
cordova build android
sdkmanager.bat "platforms;android-33"
sdkmanager.bat "build-tools;33.0.0"
cordova requirements
yarn build:release
```