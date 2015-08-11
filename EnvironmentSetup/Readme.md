
###Setting up Android Studio

1. You need to have atleast Java JDK 6.0 installed
	- If you are not sure run java -version
	- Install the latest JDK from http://www.oracle.com/technetwork/java/javase/downloads/index.html
	- Verify your installation worked by running java -version
2. Set the JAVA_HOME environment variable.
	- This varies depending on the operating system. For Unix system you need to edit your bash_profile
	- Using a text editor modify the file ~/.bash_profile (if it does not exist create it)
	-  You should add the following line to your bash profile
	- export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home where the path is the location of your Java installation
	- Save the file and run "source ~/.bash_profile"
3. Download android Studio from https://developer.android.com/sdk/index.html
4. Follow the following instructions for installation options:
	- Do not import settings.
	- Select standard settings for installation
5. Start a new Android Studio Project
	- ApplicationName: HelloWorld
	- Company Domain: Doesn’t really matter “cwallace.mobproto.com” Imagine it as a website name
	- Next
6. Select Phone and Tablet, Android API 15
8.  Blank Activity with fragment -> Next
9. Activity: HelloActivity, default for all others
10. You have know created your first Android app
