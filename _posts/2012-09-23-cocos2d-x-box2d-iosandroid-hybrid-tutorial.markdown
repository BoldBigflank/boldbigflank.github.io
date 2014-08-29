---
layout: post
status: publish
published: true
title: Cocos2d-x Box2D iOS/Android Hybrid Tutorial
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 279
wordpress_url: http://www.bold-it.com/?p=279
date: '2012-09-23 00:39:02 -0700'
date_gmt: '2012-09-23 08:39:02 -0700'
categories:
- Cocos2d
- iOS
tags: []
comments:
- id: 31
  author: Gustavo
  author_email: gustavo.nevado@gmail.com
  author_url: http://www.mocinteractive.com.br
  date: '2012-10-11 12:42:11 -0700'
  date_gmt: '2012-10-11 20:42:11 -0700'
  content: "Hi Alex,  thanks for the tutorial , i have some nightmare with the shared
    workspace in cocos2dx too , i actually upgraded to least cocos2dx-v2 , and have
    some issues with the environment. \n\nThis is my build_native.sh configuration\nNDK_ROOT=/develop/android-ndk-r8b\nCOCOS2DX_ROOT=/develop/cocos2d-2.0-x-2.0.3/Mad/Mad/libs\nGAME_ROOT=/develop/cocos2d-2.0-x-2.0.3/Mad\nGAME_ANDROID_ROOT=$GAME_ROOT/Mad/android\nexport
    PATH=$PATH:$NDK_ROOT\n\nIm receiving :\n\nAndroid NDK: jni/Android.mk: Cannot
    find module with tag 'CocosDenshion/android' in import path    \nAndroid NDK:
    Are you sure your NDK_MODULE_PATH variable is properly defined ?    \n\nIm using
    ndk8 , did you have some similar problem? \nthanks."
- id: 32
  author: farhad
  author_email: farhad@evatix.com
  author_url: ''
  date: '2012-10-18 22:50:19 -0700'
  date_gmt: '2012-10-19 06:50:19 -0700'
  content: We are using cocos2d-x 2.0.1 , there are no extension folder. so what to
    do.........
- id: 33
  author: Innich
  author_email: innich@gmail.com
  author_url: ''
  date: '2012-10-25 08:42:50 -0700'
  date_gmt: '2012-10-25 16:42:50 -0700'
  content: "I had the same problem.\nForgot to change COCOS2DX_ROOT=\"$DIR/../libs\"
    \nExcellent tutorial btw, thanks!"
- id: 34
  author: Farhad
  author_email: pdcsedu@gmail.com
  author_url: ''
  date: '2012-11-08 03:09:14 -0800'
  date_gmt: '2012-11-08 11:09:14 -0800'
  content: "Thanks for your great tutorial , it works like a charm in my game with
    cocos2d-x v2.0.1\n\nbut as now, i want to build the game with cocos2d-x c2.0.4
    but it is showing some error as below........\n\"/Users/Rakib/cocos2dx-2.0.4/testGame/testGame/android/../libs/cocos2dx/platform/third_party/android/prebuilt/libtiff/Android.mk:
    Cannot find module with tag 'extensions' in import path    \nAndroid NDK: Are
    you sure your NDK_MODULE_PATH variable is properly defined ?  \" \n\ncan you help
    me out, please???????????????"
- id: 35
  author: alex
  author_email: alex@bold-it.com
  author_url: http://www.bold-it.com
  date: '2012-12-16 18:53:47 -0800'
  date_gmt: '2012-12-17 02:53:47 -0800'
  content: Sorry, I haven't tried the latest version of Cocos2d-x.  I created this
    tutorial because the most recent previous one was a year ago.  These things seem
    to get out of date pretty quick.
- id: 36
  author: alex
  author_email: alex@bold-it.com
  author_url: http://www.bold-it.com
  date: '2012-12-16 18:57:48 -0800'
  date_gmt: '2012-12-17 02:57:48 -0800'
  content: I don't remember getting that issue.  Make sure that folder is in its correct
    place and it is defined in build_native.sh if necessary.
- id: 37
  author: federico
  author_email: federik21@tiscali.it
  author_url: ''
  date: '2013-02-07 08:56:08 -0800'
  date_gmt: '2013-02-07 16:56:08 -0800'
  content: |-
    When you say "/libs/build_native.sh, change line 40:", i though you mean the /android folder, not the libs...

    However, I get some errors, like:
    error: undefined reference to 'CGameManager::~CGameManager()'
    error: undefined reference to 'CBox2dFactory::factory'
    ecc...
- id: 38
  author: alex
  author_email: alex@bold-it.com
  author_url: http://www.bold-it.com
  date: '2013-03-19 18:04:56 -0700'
  date_gmt: '2013-03-20 02:04:56 -0700'
  content: The extensions folder is in the cocos2d-x root, you may have to check one
    directory up.
- id: 39
  author: alex
  author_email: alex@bold-it.com
  author_url: http://www.bold-it.com
  date: '2013-03-19 18:09:19 -0700'
  date_gmt: '2013-03-20 02:09:19 -0700'
  content: |-
    Thank you. I've updated the article.

    As for the errors, I'm not sure. It has been a while, I hope you've moved past these.
---
<p>How to start a Cocos2d-X project designed for both iPhone/iPad and Android</p>
<p>The Cocos2d-x project is always updating, so the latest tutorials on setting up a hybrid work environment aren't completely accurate.<br />
<br></p>
<h3>Versions for this tutorial:</h3>
<p>
Cocos2d-x: <a href="http://cocos2d-x.googlecode.com/files/cocos2d-2.0-x-2.0.2.zip">cocos2d-2.0-x-2.0.2 @ Aug 30 2012</a><br><br />
XCode: v4.5<br><br />
Android NDK: <a href="http://dl.google.com/android/ndk/android-ndk-r8b-darwin-x86.tar.bz2">Android NDK, Revision 8b (July 2012)</a><br></p>
<p>Here's the basic outline:</p>
<ol>
<li>Install Cocos2d-x</li>
<li>Install the XCode templates</li>
<li>Create an iPhone project</li>
<li>Create an Android project</li>
<li>Move the necessary Android files</li>
<li>Change the Android files to fit the new location</li>
</ol>
<h2>Install Cocos2d-x</h2>
<p>Download <a href="http://cocos2d-x.googlecode.com/files/cocos2d-2.0-x-2.0.2.zip">cocos2d-2.0-x-2.0.2 @ Aug 30 2012</a> and unzip it somewhere, such as your home directory.</p>
<h2>Install the XCode templates</h2>
<p>In the Terminal, go to the Cocos2d-x directory, then type:</p>
<p>[code lang="shell"]<br />
./install-templates-xcode.sh<br />
[/code]</p>
<p>This will give you a few options in the XCode New Project window.</p>
<h2>Create an iPhone project</h2>
<p>In XCode, click File-&gt;New-&gt;Project, create a new cocos2dx_box2d project, and name it anything (for example, 'testgame').</p>
<p><a href="http://bold-it.com/wp-content/uploads/2012/09/Screen-Shot-2012-09-23-at-12.15.26-AM.png"><img class="alignnone  wp-image-280" title="Screen Shot 2012-09-23 at 12.15.26 AM" src="http://bold-it.com/wp-content/uploads/2012/09/Screen-Shot-2012-09-23-at-12.15.26-AM.png" alt="" width="618" height="427" /></a><br></p>
<p>This will create a test game using Cocos2d-x and Box2D. Test it to make sure it runs on your system.</p>
<h2>Create an Android project</h2>
<p>First you need to set some environment variables.  In create-android-project.sh, edit the following lines near the top:</p>
<p>
[code]<br />
# set environment paramters<br />
NDK_ROOT_LOCAL=&quot;/Users/alex/android-ndk-r8b&quot;<br />
ANDROID_SDK_ROOT_LOCAL=&quot;/Users/alex/android-sdk-macosx&quot;<br />
[/code]</p>
<p>Point them to your own NDK and Android SDK paths.<br><br />
If you want to keep an NDK_ROOT environment variable:<br />
[code]<br />
export NDK_ROOT=/Users/alex/android-ndk-r8b<br />
[/code]<br />
Next, create an android project.  In Terminal, in the same directory as before:<br />
[code]<br />
./create-android-project.sh --box2d<br />
[/code]<br />
The --box2d parameter makes sure to include the Box2D library.<br />
You will be asked three questions:<br />
Identify your project<br />
[code]<br />
Input package path. For example: org.cocos2dx.example<br />
com.boldit.testgame<br />
[/code]</p>
<p>Choose what Android version you want. It will list what SDKs are available on your system. If you don't have any, <a href="http://developer.android.com/sdk/installing/index.html" target="_blank">install one</a>.</p>
<p>
[code]<br />
Now cocos2d-x supports Android 2.2 or upper version<br />
Available Android targets:<br />
...<br />
----------<br />
id: 7 or &quot;Google Inc.:Google APIs:10&quot;<br />
     Name: Google APIs<br />
     Type: Add-On<br />
     Vendor: Google Inc.<br />
     Revision: 2<br />
     Description: Android + Google APIs<br />
     Based on Android 2.3.3 (API level 10)<br />
     Libraries:<br />
      * com.android.future.usb.accessory (usb.jar)<br />
          API for USB Accessories<br />
      * com.google.android.maps (maps.jar)<br />
          API for Google Maps<br />
     Skins: WVGA854, WQVGA400, HVGA, WQVGA432, WVGA800 (default), QVGA<br />
     ABIs : armeabi<br />
----------<br />
...<br />
input target id:<br />
7<br />
[/code]</p>
<p>Last, give a name/directory for your project.</p>
<p>[code]<br />
input your project name:<br />
testgame<br />
[/code]</p>
<p>Now, test this to make sure it compiles<br />
[code]<br />
cd testgame<br />
./build_native.sh<br />
[/code]</p>
<h2>Move the necessary Android files</h2>
<p>The XCode template only copied enough over for iOS devices.  We are going to include the Android files as well.</p>
<ul>
<li>Move the <strong>&lt;COCOS2DX_ROOT&gt;/testgame/proj.android</strong> folder to the iphone project folder, next to ios.  Rename it android.</li>
<li>Copy the <strong>&lt;COCOS2DX_ROOT&gt;/external/Box2D</strong> folder into <strong>&lt;IPHONE_PROJECT&gt;/libs/</strong>, replace what is there.</li>
<li>Copy the <strong>&lt;COCOS2DX_ROOT&gt;/cocos2dx</strong> folder into <strong>&lt;IPHONE_PROJECT&gt;/libs/</strong>, replace what is there.</li>
<li>Copy the <strong>&lt;COCOS2DX_ROOT&gt;/CocosDenshion/android</strong> folder into <strong>&lt;IPHONE_PROJECT&gt;/libs/CocosDenshion/</strong></li>
<li>Copy the <strong>&lt;COCOS2DX_ROOT&gt;/extensions</strong> folder to <strong>&lt;IPHONE_PROJECT&gt;/libs/</strong>, replace what is there.</li>
</ul>
<h2>Change the Android files to fit the new location</h2>
<p>We moved the relative location of the cocos2dx folder for the Android project.  Instead of going two directories back, the cocos2dx folder is now one directory back and in the libs folder.  In &lt;IPHONE_PROJECT&gt;/android/build_native.sh, change line 40:</p>
<p>[code title="build_native.sh"]<br />
COCOS2DX_ROOT=&quot;$DIR/../libs&quot;<br />
[/code]</p>
<p>And update the LOCAL_C_INCLUDES on line 13 to include Box2D:</p>
<p>[code]<br />
LOCAL_C_INCLUDES := $(LOCAL_PATH)/../../Classes<br />
                   $(LOCAL_PATH)/../../libs/Box2d<br />
[/code]</p>
<p>Next, in android/jni/Android.mk, add a LOCAL_C_INCLUDES path to Box2D and change "$(call import-module,external/Box2D)" to "$(call import-module,Box2D)".  The result should look like this:<br />
<script src="https://gist.github.com/3772441.js"> </script></p>
<h2>Test and run</h2>
<p>Everything should be set up!  Build the project from XCode to test iOS.  Use these commands to build for android from the command line (in the new android directory)</p>
<p>[code]<br />
./build_native.sh clean<br />
./build_native.sh<br />
ant debug<br />
adb install -r bin/testgame-debug.apk<br />
adb shell am start -a android.intent.action.MAIN -n com.boldit.testgame/.testgame<br />
[/code]</p>
<p>The first two commands clean and build the cpp into java.  The `ant` command <a href="http://developer.android.com/tools/building/building-cmdline.html" target="_blank">builds</a> a debug apk for us.  The last two commands install and run the apk, respectively.</p>
<h2>FAQ</h2>
<p>This error:<br />
[code]<br />
Android NDK: /Users/alex/testgame/testgame/android/../libs/cocos2dx/platform/third_party/android/prebuilt/libcurl/Android.mk: Cannot find module with tag 'Box2D' in import path<br />
Android NDK: Are you sure your NDK_MODULE_PATH variable is properly defined ?<br />
[/code]<br />
was caused because Box2D was not completely configured.</p>
