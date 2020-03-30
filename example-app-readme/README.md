![Nevercode build status](https://app.nevercode.io/api/projects/b6c0e1f1-46b5-414a-8fe3-969670225833/workflows/6ac7f951-f9ac-4c05-9803-4f8023f17d36/status_badge.svg?branch=master&style=shields)

# Late Initialization and Reconfiguration Example 

This example app demonstrates how to late initialize and dynamically reconfigure the Thunderhead SDK on the fly.

App Flow Summary:
1. In [DynamicInitializationApplication.kt](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/dynamic-initialization-example/Dynamic%20Initialization%20Example/app/src/main/java/com/thunderhead/dynamicinitializationexample/DynamicInitializationApplication.kt#L97) `onCreate` method, the SDK is initialized with empty parameters. (*Late initialization*)
2. On initial app start, [MainActivity.kt](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/dynamic-initialization-example/Dynamic%20Initialization%20Example/app/src/main/java/com/thunderhead/dynamicinitializationexample/MainActivity.kt) is presented with no region selected/configured.  
3. The 'SELECT' button presents [ChangeRegionActivity.kt](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/dynamic-initialization-example/Dynamic%20Initialization%20Example/app/src/main/java/com/thunderhead/dynamicinitializationexample/ChangeRegionActivity.kt), which displays a list of regions to select from.
4. Upon selection of a new region, the SDK is then *reconfigured* with new API credentials corresponding to the region selected, handled in [`onActivityResult`](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/dynamic-initialization-example/Dynamic%20Initialization%20Example/app/src/main/java/com/thunderhead/dynamicinitializationexample/MainActivity.kt#L40) delegate method.  

*Note:*
- The SDK's `mode` parameter that configures `Admin Mode` is not reconfigurable on the fly, the app needs to be restarted when switching between User and Admin mode.

## Thunderhead SDK Late Initialization

In the event you want the SDK to run even without valid parameters, you can initialize the SDK with all empty strings `""` or `nil` parameters.  The SDK can then be configured later with valid parameters using the same method.

*Note:*
- In this state, the SDK locally queues end-user data and will upload the data to server once SDK is initialized with valid parameters.
- The SDK does not support partial parameters, parameters passed must either be *all* valid or *all* `empty/nil`.
    
Kotlin:
```kotlin
val builder: OneConfiguration.Builder =
            OneConfiguration.Builder()
                .siteKey("")
                .apiKey("")
                .sharedSecret("")
                .userId("")
                .host(URI.create(""))
                .touchpoint(URI.create(""))
                .mode("")
        
val oneConfiguration = builder.build()
One.configure(oneConfiguration)
```

Java:
```java
OneConfiguration.Builder builder = new OneConfiguration.Builder()
        .siteKey("")
        .apiKey("")
        .sharedSecret("")
        .userId("")
        .host(URI.create(""))
        .touchpoint(URI.create(""))
        .mode(OneModes.USER_MODE);

final OneConfiguration oneConfiguration = builder.build();
One.configure(oneConfiguration);
```
See example of usage [here](https://github.com/thunderheadone/one-sdk-android/blob/master/examples/dynamic-initialization-example/Dynamic%20Initialization%20Example/app/src/main/java/com/thunderhead/dynamicinitializationexample/DynamicInitializationApplication.kt#L97).

## Reconfiguring the Thunderhead SDK

In the case that the SDK is already initialized with valid credentials, the SDK can also be reconfigured later when necessary. This can be useful for certain situations.  For example, you may require to use different site keys or hosts corresponding to the regions your users are located in as they relocate.

To reconfigure the SDK with different parameters, simply run `One.configure()` again with the new parameters, as shown below:

Kotlin:
```kotlin
val builder: OneConfiguration.Builder =
            OneConfiguration.Builder()
                .siteKey("ONE-XXXXXXXXXX-1022")
                .apiKey("713d44a-8af0-4e79-ba7e-xxxxxxxxxxxxxxxx")
                .sharedSecret("bb8bacb2-ffc2-4c52-aaf4-xxxxxxxxxxxxxxxx")
                .userId("api@yourCompanyName")
                .host(URI.create("eu2.thunderhead.com"))
                .touchpoint(URI.create("myAppsNameURI"))
                .mode(OneModes.USER_MODE)
        
val oneConfiguration = builder.build()
One.configure(oneConfiguration)
```

Java:
```java
OneConfiguration.Builder builder = new OneConfiguration.Builder()
        .siteKey("ONE-XXXXXXXXXX-1022")
        .apiKey("713d44a-8af0-4e79-ba7e-xxxxxxxxxxxxxxxx")
        .sharedSecret("bb8bacb2-ffc2-4c52-aaf4-xxxxxxxxxxxxxxxx")
        .userId("api@yourCompanyName")
        .host(URI.create("eu2.thunderhead.com"))
        .touchpoint(URI.create("myAppsNameURI"))
        .mode(OneModes.USER_MODE);

final OneConfiguration oneConfiguration = builder.build();
One.configure(oneConfiguration);
```

## Questions or need help

### Salesforce Interaction Studio Support
_For Salesforce Marketing Cloud Interaction Studio questions, please submit a support ticket via https://help.salesforce.com/home_

### Thunderhead ONE Support
_The Thunderhead team is available 24/7 to answer any questions you have. Just email [onesupport@thunderhead.com](mailto:onesupport@thunderhead.com) or visit our docs page for more detailed installation and usage information._

