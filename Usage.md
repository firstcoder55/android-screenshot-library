# What is this? #

Android Screenshot Library (ASL) provides means for taking snapshots of phone's screen without the need for signing your application or having privileged (root) access to the Android system. It is intended primarly for taking screenshots used for testing, debugging and diagnostics.


# How does it work? #

ASL utilizes background native service which performs screen capturing on demand from an application that uses the library. This service has to be started using Android Debug Bridge (ADB), which is an utility program bundled with Android SDK. The service provides screenshot-taking functionality for any application that uses ASL for as long as the phone isn't rebooted, regardless of whether or not it is connected to the PC.


# Contents of package #

Android Screenshot Library consists of the following files:

  * Java-related files used by client applications:
    * _ScreenshotService.java_, which contains Android service class communicating with the native service
    * _IScreenshotProvider.aidl_, which contains definition of interface used by client application
  * _asl-native_ - Native service binary which has to be installed on the phone & ran by ADB
  * Scripts for various shells that install and start the native service:
    * _run.sh_ - /bin/bash script for Unix-like operating systems
    * _run.ps1_ - PowerShell script recommended for Windows systems
    * _run.bat_ - Batch script for Windows systems
  * _demo_ folder, containing a sample Android application which uses the Android Screenshot Library


# Using the API #

Refer to [DeveloperGuide](DeveloperGuide.md) for details about embedding ASL in your own application and using the programming interface it exposes.

# Starting the native service #

Refer to [UserGuide](UserGuide.md) for details about using the screenshot capturing features of ASL in applications.