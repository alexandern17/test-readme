# Late Initialization and Reconfiguration Example 

This example app demonstrates how to late initialize and dynamically reconfigure the Thunderhead SDK on the fly.

## Thunderhead SDK Late Initialization

In the event you want the SDK to run even without valid parameters, you can initialize the SDK with all empty strings `""` or `nil` parameters.  The SDK can then be configured later with valid parameters using the same method.

*Note:*
- In this state, the SDK locally queues end-user data and will upload the data to server once SDK is initialized with valid parameters.
- The SDK does NOT support partial parameters, parameters passed must either be *all* valid or *all* `empty/nil`.
    
Swift:
```swift
One.startSessionWithSK("",
    uri:"",
    apiKey:"",
    sharedSecret:"",
    userId:"",
    adminMode: false,
    hostName:"")
```

Objective-C:
```objective-c
[One startSessionWithSK:@""
                uri:@""
             apiKey:@""
           sharedSecret:@""
             userId:@""
              adminMode:NO
               hostName:@""];
```

## Reconfiguring the Thunderhead SDK

In the case that the SDK is already initialized with valid credentials, the SDK can also be reconfigured later when necessary. This can be useful for certain situations.  For example, you may require to use different site keys or thinstances corresponding to the regions your users are located in as they relocate.

To reconfigure the SDK with different parameters, simply run `One.startSessionWithSK` again with the new parameters, as shown below:

Swift:
```swift
One.startSessionWithSK("ONE-XXXXXXXXXX-1022",
    uri:"myAppsNameURI",
    apiKey:"f713d44a-8af0-4e79-ba7e-xxxxxxxxxxxxxxxx",
    sharedSecret:"bb8bacb2-ffc2-4c52-aaf4-xxxxxxxxxxxxxxxx",
    userId:"api@yourCompanyName",
    adminMode:false,
    hostName:"eu2.thunderhead.com")
```

Objective-C:
```objective-c
[One startSessionWithSK:@"ONE-XXXXXXXXXX-1022"
                uri:@"myAppsNameURI"
             apiKey:@"f713d44a-8af0-4e79-ba7e-xxxxxxxxxxxxxxxx"
           sharedSecret:@"bb8bacb2-ffc2-4c52-aaf4-xxxxxxxxxxxxxxxx"
             userId:@"api@yourCompanyName"
              adminMode:NO
               hostName:@"eu2.thunderhead.com"];
```

## Installation

### CocoaPods

Make sure you have the [CocoaPods](http://cocoapods.org) dependency manager installed. You can do so by executing the following command:

```sh
$ gem install cocoapods
```

In order to run the app, install the Thunderhead SDK into the Example App using the following command:

```sh
$ pod install
```

## Questions or need help

_The Thunderhead ONE team is available 24/7 to answer any questions you have. Just email onesupport@thunderhead.com or visit our docs page for more detailed installation and usage information._
