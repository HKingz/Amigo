#Amigo Usage

[中文版](https://github.com/eleme/Amigo/blob/master/README_zh.md#amigo)
[wiki](https://github.com/eleme/Amigo/wiki)

![amigo.png](http://amigotheband.com/wp-content/uploads/2015/02/logo_amigo-yellow.png)  

Amigo is a hotfix library which can hotfix almost everything for your app.

## Usage
In your project's `build.gradle`

```groovy
dependencies {
  classpath 'me.ele:amigo:0.0.7'
}
```
In your module's `build.gradle`

```
 apply plugin: 'me.ele.amigo'
```

you are good to go now, as simple as this.

### notice 

sync with jcenter may take some time, if amigo cannot be found, please add my private maven url into your buildscript

```groovy
buildscript {
    repositories {
        maven {
            url "https://dl.bintray.com/jackcho/maven"
        }
        jcenter()
        ...
    }
}
```

### to make hotfix work
There are two ways to make hotfix work.

* if you don't need hotfix work immediately

	you just need to download new apk file to /data/data/{your pkg}/files/amigo/demo.apk,
	when app restarts next time, hotfix apk will be loaded as fresh as new.

	```java
	File hotfixApk = Amigo.getHotfixApk(context);
	FileUtils.copyFile(yourApkFile, hotfixApk);
	
    Amigo.workLater(context);

    Amigo.workLater(context, apkFile);
    ```

* work immediately, app will restart immediately

	```java
	Amigo.work(context);

	Amigo.work(context, apkFile);
	```


### maybe hotfix needs to be cleared

```java
Amigo.clear(context);
```
**note**：if apk has changed we will automatic clear the old apk.

### customize the fix layout
some time-tense operation is handled in a new process with an activity, you may customize it

```xml
<meta-data
    android:name="amigo_layout"
    android:value="{your-layout-name}" />

<meta-data
    android:name="amigo_theme"
    android:value="{your-theme-name}" />

```

### load new Activity and BroadcastReceiver

you can add activities & receivers whatever you like to add in your hotfix apk,
waiting for **Service** & **ContentProvider**

if you would like to RTFC, please checkout **support_new_added_components** branch

this's in **beta** version for now, so you may use this

```groovy
 classpath 'me.ele:amigo:0.0.6-beta1'
 ...

```

play with demo
----

if you try to experience Amigo's magic, you can integrate with your own app as you like;
also you can play with this app demo following the procedures below.

   1. ./gradlew clean assembleRelease & adb install .../build/outputs/apk/app-release.apk
   2. change code wherever you like & ./gradlew clean assembleRelease
   3. adb push .../build/outputs/apk/app-release.apk /sdcard/demo.apk
   4. kill Amigo demo by yourself & restart to check if your change works
   
### retrieve hotfix file

- make it simple, you just need a fully new apk

- for user's network traffic's sake, you may just want to download a diff file
  [bspatch](https://github.com/eleme/bspatch) is an option for you


license
====

	  Copyright 2016 ELEME Inc.

	  Licensed under the Apache License, Version 2.0 (the "License");
	  you may not use this file except in compliance with the License.
	  You may obtain a copy of the License at

	     http://www.apache.org/licenses/LICENSE-2.0

	  Unless required by applicable law or agreed to in writing, software
	  distributed under the License is distributed on an "AS IS" BASIS,
	  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	  See the License for the specific language governing permissions and
	  limitations under the License.
