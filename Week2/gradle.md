##What is Gradle?

**Gradle is a build system.** It manages dependencies, and converting code into files usable by the JVM.
It is written in Groovy, and you yourself can write scripts in it. (Though for this class you won't have to)

Gradle is similar to Maven or Ant, but both Maven and Ant define dependencies and tasks in XML code

Adroid has a plugin for gradle that handles most of the dirty work for us. For the purposes of this class it is likely that you will only use gradle for dependency management. 

That being said gradle is incredibly powerful and can be used for building tons of applications, testing applications and working with continuous integration

###build.gradle file

build.gradle files are build configuration files for gradle. When gradle is ran, it looks for a build.gradle file and reads tasks from there. We will look at the below file to show how tasks are defined

```Groovy
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "21.1.2"

    defaultConfig {
        applicationId "com.example.cwallace.grocerylist"
        minSdkVersion 15
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.0.1'

}
```

There are two items defined in this file: 
the task android and dependencies.

The android task sets parameters, such as minSdkTarget  that are then consumed by the run configuration.

###What is the run configuration?

When you hit the play button you are actually running a specific configuration that you have defined. In Android studio it is defaulted to an Android run configuration. You can look at parameters that are specified by going into Play button’s drop down menu and selecting the configuration “app”

You shouldn’t have to change anything in there, but in non android projects or when you are writing test code you may create additional configurations and tasks that are used to run tests are deploy servers.

###What do we need to know.

Gradle manages your dependencies. The only reason Android Studio knows which classes to import and what methods it has it because gradle is telling it all the places to look.

Realistically you are only going to have to modify dependencies. Dependencies come from two places. Either locally or a remote repo. 

jcenter() specifies the remote repo that will be used. jcenter is the default remote repository.

to include a dependency that is located in a remote repository, you can find the dependency name on this website. 
http://mvnrepository.com/
Also, googling a phrase like "Apache Http gradle" will generally allow you to find the name of the dependency you need to import.

Once you have the name you need to put it in the dependencies section under compile

```Groovy
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:23.0.1',
	    ‘YOUR PACKAGE’

}
```

The second places dependencies come from is locally. That is what the line
```
 compile fileTree(dir: 'libs', include: ['*.jar'])
 ```
  is for. It should compile any .jar files in a directory called /libs and allow you to use them in code.

This occasionally gets tricky if the extension is not .jar, but for the most part this should work.


###'com.mcxiaoke.volley:library:1.0.18' 

this is the dependency for volley you will need to include this in your build.gradle file



