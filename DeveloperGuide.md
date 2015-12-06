ASL programming interface consists of Android service accessible via RPC using the `pl.polidea.asl.IScreenshotProvider` interface. The interface is defined in _IScreenshotProvider.aidl_ file which has to be included in the build process. Similarly, _ScreenshotService.java_, which contains the Android service's code, has to be added to he client projects codebase as well.

# Modifying the manifest XML #
In order for Android service to be accessible, add the following declaration to your client application's XML manifest:

```
<service android:name="pl.polidea.asl.ScreenshotService">
	<intent-filter>
		<action android:name="pl.polidea.asl.ScreenshotService.BIND" />
		<category android:name="android.intent.category.DEFAULT"/>
	</intent-filter>
</service>
```

# Binding service #

To obtain the `IScreenshotProvider` interface one must bind to the ASL service (`pl.polidea.asl.ScreenshotService`) using `Context.bindService` - for example:

```
// (using class name)
Intent intent = new Intent();
intent.setClass (this, pl.polidea.asl.ScreenshotService.class);
bindService (intent, aslServiceConnection, Context.BIND_AUTO_CREATE);
```

or

```
// (using BIND action)
bindService (new Intent(pl.polidea.asl.ScreenshotService.BIND), aslServiceConnection, Context.BIND_AUTO_CREATE);
```

`aslServiceConnection` is an object deriving from `ServiceConnection` class and serving as a callback for when the connection with the service is established. There you can obtain the `IScreenshotProvider` interface from `IBinder` you receive:

```
private IScreenshotProvider screenshotProvider = null;
private ServiceConnection aslServiceConnection = new ServiceConnection() {
    @Override
    public void onServiceConnected(ComponentName name, IBinder binder) {
        screenshotProvider = IScreenshotProvider.Stub.asInterface(binder);
    }
    @Override
    public void onServiceDisconnected(ComponentName name) { }
};
```

# `IScreenshotProvider` interface #

`IScreenshotProvider` interface is very simple -- it has only two methods:
  * `isAvailable`, which checks whether the native service is up and running; returns `boolean` value
  * `takeScreenshot`, which performs screen capturing and stores result in a ._png_ file on the SD card. Method returns full path to file containing the newly captured screenshot. The image doesn't have any compression applied to it for maximum pixel consistency.