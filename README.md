# Dynamic Initialization Example 

This example app demonstrates how to reconfigure ONE SDK parameters on the fly.

## Initializing the ONE SDK

You can initialize the SDK with either all valid or empty/nil parameters.
- When initialized with valid credentials, the SDK can be reconfigured later when deemed necessary.
- When initialized by passing all `empty strings` or `nil` parameters (late initialization), the SDK can be then be configured with valid parameters later using the same method.
	- Note: In this state, the SDK locally queues end-user data and will upload the data to server once SDK is initialized with valid parameters.

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

Note: SDK cannot initialize with partial parameters, all parameters need to exist and be valid.

## Reconfiguring ONE SDK Parameters

To reconfigure the SDK with different site credentials, simply run `One.startSessionWithSK` again with the new parameters.

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

Install the One SDK into the Example App using the following command:

```sh
$ pod install
```

## Questions or need help

_The Thunderhead ONE team is available 24/7 to answer any questions you have. Just email onesupport@thunderhead.com or visit our docs page for more detailed installation and usage information._
