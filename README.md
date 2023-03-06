# datarius-android-sdk-releases

Public releases for AudienceM Android SDK

## Installation

### Step 0. Create github token

Go to https://github.com/settings/tokens and create a classic token with read:packages permission.

Use that token below

### Step 1. Add the Analytics dependency to your build.gradle

The recommended way to install the library for Android is with a build system like Gradle. This makes it dead simple to upgrade versions and add integrations. The library is distributed via Github Packages. 

Add repository to your settings.gradle:
```
dependencyResolutionManagement {
    repositories {
        maven {
            url 'https://maven.pkg.github.com/flescorp/datarius-android-sdk-releases'
            credentials {
                username = "<your github username>"
                password = "<your github token>"
            }
        }
    }
}
```

Add the analytics module to your app/build.gradle:
```
dependencies {
    implementation 'kr.co.fles.datarius.kotlin:android:1.10.3'
}
```

### Step 2. Initialize the Client

We recommend initializing the client in your Application subclass.

```
// Create an analytics client with the given application context.
// NOTE: in android, application context is required to pass as the second parameter.
Analytics(applicationContext) {
    // Automatically track Lifecycle events
    trackApplicationLifecycleEvents = true
    flushAt = 3
    flushInterval = 10
}
```

Automatically tracking lifecycle events (Application Opened, Application Installed, Application Updated) is optional, but highly recommended to hit the ground running with core events!

### Step 3. Add Permissions to AndroidManifest.xml

```
<!-- Required for internet. -->
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

## Usage

### Identify

Java `Analytics.with(context).identify("a user's id", new Traits().putName("홍길동"), null);`

Kotlin `Analytics.with(context).identify("a user's id", Traits().putName("홍길동"), null)`

### Track

Kotlin
```
Analytics.with(context).track("Product Viewed", Properties().putValue("name", "Moto 360"))

```

###  Screen

Kotlin
```
// category "Feed" and a property "Feed Length"
Analytics.with(context).screen("Feed", Properties().putValue("Feed Length", "26"))

// no category, name "Photo Feed" and a property "Feed Length"
Analytics.with(context).screen(null, "Photo Feed", Properties().putValue("Feed Length", "26"))

// category "Smartwatches", name "Purchase Screen", and a property "sku"
Analytics.with(context).screen("Smartwatches", "Purchase Screen", Properties().putValue("sku", "13d31"))
```

### Group

Kotlin
```
Analytics.with(context).group("a user's id", "a group id", Traits().putEmployees(20))
```

### Alias
Kotlin
```
Analytics.with(context).alias(newId)
Analytics.with(context).identify(newId)
```
