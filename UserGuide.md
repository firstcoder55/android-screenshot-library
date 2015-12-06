# Introduction #

For ASL to work, it requires native service running on the device in background. This service has to be installed & started using the Android Debug Bridge (ADB), which is part of Android SDK library. This requirement is motivated by Android platform's security constraints.
Fortunately, installation & start-up of native service is easy and has to be performed only once per device boot.

# Starting native service #

If the service isn't running on the device yet (i.e. it just have been rebooted), there are few steps to be taken before ASL screen-capturing functions may work.

  1. Make sure your system has the Android SDK installed. You can always find current SDK  [here](http://developer.android.com/sdk/index.html).
  1. Set `ANDROID` environmental variable to the root directory of your Android SDK (for example _C:\Android_ or _/var/lib/google/android-sdk_).
  1. Execute one of the _run.xxx_ scripts included in the ASL package, appropriate for your operating system and shell:
    * for Windows systems, _run.ps1_ (PowerShell script) is recommended. There is also Batch script under _run.bat_.
    * for Unix-based systems (like Linux or OSX), _run.sh_ can be used.
  1. Follow the instructions, prompting you for connecting the phone. (You can also have it connected earlier).
  1. When the service has been successfully started, you are free to unplug the phone from your PC.

That's it. The native service will be active as long as the phone does not reboot itself.