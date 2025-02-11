﻿This document describes how to quickly integrate the Tencent Cloud IM SDK to your projects. To configure and integrate the SDK, follow these steps.
## Environment Requirements
- JDK 1.6.
- Android 4.1 (SDK API level 16) or above

## Integrating the SDK (AAR)
You can use Gradle to automatically load the AAR file or manually download the AAR file and import it into your project.

### Method 1: automatic loading (AAR)
Because the JCenter service will be deprecated, subsequent IM SDKs will be published to the Maven Central repository. You can configure Gradle to automatically download updates.
Use Android Studio to open your project and modify the `app/build.gradle` file in three simple steps to integrate the SDK to your project, as shown below:

- **Step 1: add SDK dependencies**

 Find `build.gradle` of the app and add `mavenCentral()` dependencies to `repositories`.
```
 repositories {
        google()
        jcenter()
        // Add the `mavenCentral` repository.
        mavenCentral()
 }
```
 Add the IM SDK dependencies to `dependencies`.
 If the IM SDK basic edition is used, add the following dependencies:
```
dependencies {
		api 'com.tencent.imsdk:imsdk:version number'
}
```
If the IM SDK enhanced edition is used, add the following dependencies:
```
dependencies {
		api 'com.tencent.imsdk:imsdk-plus:Version number'
}
```
>?Replace `version number` with the actual version number of the SDK. You are advised to use the [latest version]( https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK).
>Take the version number `5.4.666` as an example:
>```
dependencies {
		api 'com.tencent.imsdk:imsdk-plus:5.4.666'
}
```
>

- **Step 2: specify the app architecture**
In `defaultConfig`, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported starting from IM SDK v4.3.118).
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

- **Step 3: sync the SDK**
Click the `Sync` icon. If the connection to JCenter is normal, the SDK will be automatically downloaded and integrated to your project.
![](https://main.qcloudimg.com/raw/2e281799c00da2dba59551ff26c6561e.png)


### Method 2: manual download (AAR)
If JCenter cannot be accessed, you can manually download the SDK and integrate it into your project:
- **Step 1: download the IM SDK**
Download the latest version of the [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK) from GitHub.

- **Step 2: copy the IM SDK to the project directory**
Copy the downloaded AAR file to the **/libs** directory of the project.
![](https://main.qcloudimg.com/raw/4175f483d55c2f99b99c993ada8dd5a0.png)

- **Step 3: specify the architecture used by the app and compile and run the architecture**
In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported starting from IM SDK v4.3.118).
```
defaultConfig {
	ndk {
		abiFilters "arm64-v8a"
	}
}
```


## Integrating SDK
If you do not want to integrate the AAR library, you can integrate the IM SDK by importing the JAR and SO libraries.

- **Step 1: download and decompress the IM SDK**
[Download](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK) the latest version of the AAR file from GitHub and decompress it. The extracted folder contains a JAR file and an SO subfolder. Rename **classes.jar** to **imsdk.jar**.
![](https://main.qcloudimg.com/raw/ecc6ae484565b0170c42698825951eba.png)

- **Step 2: copy the SDK files to the project directory**
Copy the renamed JAR file and SO files of different architectures to the default loading directories of Android Studio.
![](https://main.qcloudimg.com/raw/237b44da2ec04ba87a6cef66aa0b5321.png)

- **Step 3: specify the architecture used by the app and compile and run the architecture**
In the `defaultConfig` of `app/build.gradle`, specify the CPU architecture used by the app (armeabi-v7a, arm64-v8a, x86, and x86_64 are supported starting from IM SDK v4.3.118).
```
   defaultConfig {
        ndk {
            abiFilters "arm64-v8a"
        }
    }
```

## Configuring App Permissions
To configure app permissions in `AndroidManifest.xml`, the IM SDK requires the following permissions:

```
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

## Configuring Obfuscation Rules
In the `proguard-rules.pro` file, add the IM SDK classes to the "do not obfuscate" list.

```
-keep class com.tencent.imsdk.** { *; }
```

