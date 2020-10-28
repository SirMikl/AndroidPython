# AndroidPython
Python with Java
Gradle plugin
In the project’s top-level build.gradle file, add the Chaquopy Maven repository and dependency to the end of the existing repositories and dependencies blocks:
buildscript {
    repositories {
        ...
        maven { url "https://chaquo.com/maven" }
    }
    dependencies {
        ...
        classpath "com.chaquo.python:gradle:8.0.1"
    }
}
Then, in the module-level build.gradle file (usually in the app directory), apply the Chaquopy plugin at the top of the file, but after the Android plugin:
apply plugin: 'com.android.application'
apply plugin: 'com.chaquo.python'        // Add this line
All other configuration will be done in this module-level build.gradle. The examples below will show the configuration within defaultConfig, but it can also be done within a product flavor.
The Chaquopy plugin can also be used in an Android library module (AAR). However, it can only be used in one module in a project: either in the app module, or in exactly one library module. Attempting to use it in multiple modules will give the error “More than one file was found with OS independent path”.


applicationId "com.example.pythonforandroid"
sourceSets{
    main{
        python{
            srcDirs = ["src/main/python"]
        }
    }
}

ndk {
       abiFilters "armeabi-v7a", "x86"
    }

python{
    buildPython "C:/Python38/python.exe"
}


if (!Python.isStarted()){
    Python.start(new AndroidPlatform(this));
Python py = Python.getInstance();


