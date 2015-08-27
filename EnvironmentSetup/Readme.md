# MobileProto2015-Environment-Setup

It is likely easiest to do this class on a Mac/Linux machine. However, many people also can install Android studios on a Windows machine and do not have an issue with it.  

### Installing Java

You must install the Java JDK to develop for android. To do so follow the link http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html and download the file for your approprtiate operting system. If your machine is a 64 bit system (It probably is) you will want to install the option with x64 after it. 

1. After installing the JDK you must set the JAVA_HOME envrionment variable on your system. On a Windows machine:
  - Select Start menu > Computer > System Properties > Advanced System Properties. Then open Advanced tab > Environment Variables and add a new system variable JAVA_HOME that points to your JDK folder, for example C:\Program Files\Java\jdk1.7.0_21.
  - On a Mac/Linux you must edit your bash_profile.
    1. nano ~/.bashrc
    2. Add a the line " export JAVA_HOME=/usr/java/jdk1.5.0_07/bin/java" that points to the location of your JDK. 
    3. Ctrl C
    4. Hit the button y, and then enter
    5. run command: source ~/.bashrc

### Installing Android studio

1. Download Android Studio from https://developer.android.com/sdk/index.html#Other
2. https://developer.android.com/sdk/installing/index.html?pkg=studio Contains steps for installing Android Studio for all operating system. We will give instructions for a Linux machine.
3. Unpack the downloaded tar file 
  - tar zxf $DIRECTORY/android-sdk_r24.3.4-linux.tgz -C /opt
4. To run android studio you will need to run the command /opt/android-studio/bin/studio.sh
  - You may want to consider either creating an alias for this command or add /opt/android-studio/bin to your PATH. Instructions for either exist here: 
  - http://askubuntu.com/questions/17536/how-do-i-create-a-permanent-bash-alias?lq=1
  - http://stackoverflow.com/questions/7360889/adding-a-directory-to-path-in-ubuntu

### Android Studio Configuration

1. Open Android Studio
2. Do not import settings
3. Select standard settings for installation
4. Start a new Android Studio Project
5. Naming:
  - ApplicationName: HelloWorld
  - Company Domain: Doesn’t really matter “cwallace.mobproto.com” Imagine it as a website name
6. Select Phone and Tablet, Android API 15
7.  Blank Activity with fragment -> Next
8. Activity: HelloActivity, default for all others

### Create an emulator

If you do not have an Android phone you will need an emaultor to test your apps. Even if you have one, you may like to use the emulator isntead of your phone

Note:
On a Windows machine you will have to install Intel HAXM. Instructions to do so can be found on this page http://developer.android.com/tools/devices/emulator.html#acceleration under "Configuring VM Acceleration on Windows"

1. Go to Tools > Android > AVD Manager
2. Create a virtual device and select a phone (truthfully the phone does not matter now)
3. Select a name for the emulator and keep the default options
4. Select finish

###Running an application

1. To run an app press the play button at the top of the screen.
2. This will prompt a screen where you can either select a running device or launch an emulator.
  - A running device will either be a phone that is plugged into your computer and in debug mode or an emulator you already launched
3. Select a device and select ok
4. Your application should appear on the emulator or your device.
