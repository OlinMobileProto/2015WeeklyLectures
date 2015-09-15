## Android Manifest 

The Android Manifest is an XML file necessary for your app to work. It specifies parameters that are used by the android system.  Below is an example manifest file
```XML
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.photos.cwallace.photostreamapp" >
    <uses-permission android:name="android.permission.INTERNET" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name=".PhotosActivity"
            android:label="@string/app_name" >
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
The reason you will most likely have to interact with this file is to set permissions for your application.

### Setting Permissions

http://developer.android.com/reference/android/Manifest.permission.html

That link contains a list of all the available permissions you can set on your application. You should notice that one of them is an internet permission.
To access the internet you will need to add this line
```
<uses-permission android:name="android.permission.INTERNET" />
```
to your manifest, as is done in the sample manifest file above. You would do the same for any other permission you needed.

### Set default activity

You also specify the name and location of the default activity that should be loaded when your application loads. This should be done correctly for you when you create your app, but if you wish to change the default activity you will need to change the values in the activity xml tag.