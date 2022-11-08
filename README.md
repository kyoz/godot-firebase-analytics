# Firebase Analytics plugin for godot engine

Use [NativeLib Addon](https://github.com/DrMoriarty/nativelib) or [NativeLib-CLI](https://github.com/DrMoriarty/nativelib-cli) for installation.

It supports Android and iOS.
Don't forget to enable Android and/or iOS platform in NativeLib before installing this plugin.

## For iOS

Ensure that plugin `NativeLib-Export` installed and enabled

Add `GoogleService-Info.plist` in `addons/nativelib-export/iOS` (you could download it from the firebase console where you manage platforms of your project)

## For Android

You should put `google-services.json` into `android/build` folder.

The `google-services.json` you could download from your firebase console where you manage platforms of your project.

Inside your custom build `build.gradle` (inside `android/build`) add theses:

```
...
    dependencies {
        classpath libraries.androidGradlePlugin
        classpath libraries.kotlinGradlePlugin
        classpath 'com.google.gms:google-services:4.3.14'    <=== Add this
//CHUNK_BUILDSCRIPT_DEPENDENCIES_BEGIN
//CHUNK_BUILDSCRIPT_DEPENDENCIES_END
    }

...


//CHUNK_DEPENDENCIES_BEGIN
//CHUNK_DEPENDENCIES_END
}

apply plugin: 'com.google.gms.google-services'    <=== And this

android {
    compileSdkVersion versions.compileSdk
    buildToolsVersion versions.buildTools
...
```


# Usage

The plugin's script will be automatically added to your autoloading list. So you will get global object `fba` with methods described below.

# API

## screen(name: String, screen_class: String)

Inform that user open this screen.

## setUserId(id: String)

Set custom user id

## logEvent(event: String, params: Dictionary = {})

Log specific event in you application. Params is optional.

## userProperties(props: Dictionary)

Set user properties. Firebase will store the last value for every property.

## start_checkout(item_id: String, item_name: String, item_category: String, price: float, currency: String = 'USD')

Inform that user starts purchasing in your app.

## revenue(price: float, quantity: int, product: String, currency: String = 'USD', signature: String = '', receipt: String = '')

Inform that user finished purchasing. Optionally you could provide signature and receipt for purchase verification.
