# Orchestration optimization example

This example app demonstrates how to use the ochestration optimization feature in the Thunderhead SDK.
For the tutorial to set up this example app, see [here](https://na5.thunderhead.com/one/help/conversations/how-do-i/mobile/android-orchestrations/one_integrate_mobile_android_orch_intro/).

### How to run

The parameters found in the `gradle.properties` file is used as configuration parameters for the Thunderhead SDK, which is configured in [OptimizationApp.kt](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/optimizing-programmatically-using-json-example/app/src/main/java/com/thunderhead/optimizationexample/OptimizationApp.kt).

* Clone this repo or download the source directly.
* Update configuration values in `gradle.properties` with your Thunderhead credentials:
```java
thunderheadAdminMode=false
thunderheadUser="user@tenant"
thunderheadApiKey="my-key"
thunderheadSharedSecret="my-secret"
thunderheadSiteKey="my-site-key"
thunderheadTouchpoint="android://thunderheadDemo"
thunderheadHost="https://xx.thunderhead.com"
```
* Open project in Android Studio
* Clean and Build the Project
* Play the "App" on an emulator

### App Flow Summary

The app is a simple `TabView` based app with 2 fragment screens:

 * [FirstFragment](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/optimizing-programmatically-using-json-example/app/src/main/java/com/thunderhead/optimizationexample/MainActivity.kt#L68)
	* Contains a `RecyclerView` which displays a list of product images. 3 products are displayed in the list and are linked to images found under the app assets folder.
	* This will be the area which we will optimize based on JSON content received from ONE.
	* Tapping a recycler item cell in the second tab will send a response code to ONE to record the user sentiment for the optimization asset shown.
 * [SecondFragment](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/optimizing-programmatically-using-json-example/app/src/main/java/com/thunderhead/optimizationexample/MainActivity.kt#L222)
 	* Contains a simple set of buttons which will help us record the app user interest similar to how this could be achieved in your app.

### Migrating from versions < 6.0.0

Version 6.0.0 of the Thunderhead SDK introduced static methods and Kotlin top-level extension functions.
Please see below to see how to migrate the SDK methods used in this example app from < 6.0.0.  

#### Configuring the SDK

```kotlin
 // Old 

 One.getInstance(this)?.run {
	init(
		BuildConfig.thunderheadSiteKey,
		BuildConfig.thunderheadTouchpoint,
		BuildConfig.thunderheadApiKey,
		BuildConfig.thunderheadSharedSecret,
		BuildConfig.thunderheadUser,
		BuildConfig.thunderheadHost,
		if(BuildConfig.thunderheadAdminMode) OneModes.ADMIN_MODE else OneModes.USER_MODE
	)
}
```

```kotlin
 // New

oneConfigure {
	siteKey = BuildConfig.thunderheadSiteKey
	apiKey = BuildConfig.thunderheadApiKey
	sharedSecret = BuildConfig.thunderheadSharedSecret
	userId = BuildConfig.thunderheadUser
	host = URI(BuildConfig.thunderheadHost)
	touchpoint = URI(BuildConfig.thunderheadTouchpoint)
	mode = if(BuildConfig.thunderheadAdminMode) OneModes.ADMIN_MODE else OneModes.USER_MODE
}
```
