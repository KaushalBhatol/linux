# ADB

## alias - basic defined

* local  = pc     = ~/Desktop/
* remote = mobile = sdcard/mobile.txt

## Basic commands

    adb devices # listed all connected devices
    adb shell # launches a shell on the device
copying pc file to android:

    adb push local remote
copying android file to pc:

    adb pull remote [local]

## installing apk

    adb install file.apk

## logs in realtime

View the device log in real-time:

    adb logcat  
You can use adb logcat `-b` radio to view radio logs, and adb logcat `-C` to view logs in colour
