# 0. Put artifact at www folder
```
mkdir www
cp -rp artifact www/
```
# 1. Install Cordova

```
npm install -g cordova
cordova platform add android
```

# 2. Install Android Development Tools

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

```bash:
export JAVA_HOME=<java-location>
export ANDROID_SDK_ROOT=<sdk-location>
export PATH=$PATH:$ANDROID_SDK_ROOT/platform-tools/
export PATH=$PATH:$ANDROID_SDK_ROOT/tools/
export PATH=$PATH:$ANDROID_SDK_ROOT/emulator/
```
# 3. Check
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

# 4. Build
```
cordova build
```
# 5. Test in Emulator
1. Create a Device

    Android Studio - Virturl Device Manager - Create Device
2. Run App
```
cordova run android --emulator
```

