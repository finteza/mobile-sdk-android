# FintezaSDK for Android 

## Installation and initialization

Finteza SDK operation requires Android 4.0.3 (API Level 15) or higher and com.android.installreferrer:installreferrer library. The SDK can be installed using Gradle or manually by downloading the package at https://bintray.com/finteza/maven/finteza-sdk.


### Installation via Gradle

To connect Finteza SDK, add the following dependency to the dependencies section of the build.gradle file of your project:

```
dependencies {
   //... other dependencies
    implementation 'net.metaquotes.finteza:finteza-sdk:+'
}
```

### Manual installation

Download the latest SDK version as a jar file and copy it to the libs directory of your project. Next, add the SDK jar file to the project as a library.

Add the following service to the project manifest:

```<service android:name="net.metaquotes.FintezaService" />```

Add permissions:

```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

Next, add the following dependency to the build.gradle file:

```
dependencies {
   //... other dependencies
    implementation 'com.android.installreferrer:installreferrer:1.0'
}
```

## Initializing SDK in the application

To initialize, call the Finteza.initialize method in the Application.onCreate or Activity.onCreate handler:

```Finteza.initialize(getApplication(), "{WEBSITE_ID}", "{WEBSITE_URL}", "{PRODUCT}");```

Set the website ID as {WEBSITE_ID}. It can be obtained in the website settings (ID field) of the Finteza panel. Next, set the parameters:

Parameter | Type | Description
site | string | Website domain name, for example, "my.site.com".
product | string | Product name to be used as a prefix for labeling events sent to Finteza by your application.

You may need it to separate events across different platforms in case you have apps for PC, iOS, Android, etc. For example, if you specify the "Android App" product and send "Registration" event, the final event name in Finteza will be "Android App Registration".

Set null to avoid using prefix.
## Application launch events 

Add the following code to Activity.onCreate:

```Finteza.activate()```

When activate is called at the first application start, SDK sends the "Install Finish" event to Finteza (if product prefix is specified, "{PRODUCT} Install Finish" is sent).

Also, when calling activate, a new working session starts and the "Session Start" event is registered (if the product prefix is set, then "{PRODUCT} Session Start").

If a user leaves the application, the current session ends. The next time the application is launched/activated, a new session begins.
	
## Debugging messages

To test SDK operation, you can enable the output of debugging information to the developer console, filtered by message type:

### Events only

```Finteza.addLogging(LogUtil.LogLevel.EVENTS);```

### Full logging

```Finteza.addLogging(LogUtil.LogLevel.ALL);```

### Errors only

```Finteza.addLogging(LogUtil.LogLevel.ERROR);```

To disable debugging messages, call:

```Finteza.addLogging(LogUtil.LogLevel.NONE);```

### Example

The following debugging message indicates an event sending error due to the absence of the activate method call:

[event] cannot send event 'Book Load': call the 'activate' method first

## NEXT

For further settings and examples please proceed to official documentation page https://www.finteza.com/en/integrations/android-sdk 
