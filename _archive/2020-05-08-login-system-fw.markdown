---
layout: post
title: "Open source social login libraries for Android"
categories: [programming, java, android, open source]
---

>Test session aiming to take a general look on how social login libraries scattered around Github are doing what they promise to do

- First things first, using `soial login libraries for Android` as search keyword displays quite many links. Using `Github` as an additional search key landed to around half dozen repository links. Churned them down to ~~four~~ three in the end.

## Initial impressions

### [SimpleAuth](https://github.com/jaychang0917/SimpleAuth) by [jaychang0917](https://github.com/jaychang0917)

- Works for Facebook, Google, Twitter and Instagram.
Instagram too has an Authentican API as it turns out, and is based on [OAuth 2.0 protocol](tools.ietf.org/html/draft-ietf-oauth-v2-12). Documentation can be found [here](https://www.instagram.com/developer/authentication/).

- Is in archived state, latest commit some 2 years ago. Still uses `compile` instead of `implementation` to add new dependencies, as stated in README.md file.

> `compile` is replaced with `api` for transitivity, else `implementation`. Basically, the `api` prefix exposes the dependency as interface to the consumer; whereas `implementation` uses the dependency strictly for internal use only.


| Name | Role                 | Consumable? | Resolveable? | Description                             |
| api | Declaring API dependencies            |      no     |      no      | This is where you should declare dependencies which are transitively exported to consumers, for compile.        |
| implementation | Declaring implementation dependencies           |      no     |      no      | This is where you should declare dependencies which are purely internal and not meant to be exposed to consumers.                |
| compileOnly | Declaring compile compile only dependencies    |     yes     |      yes     | This is where you should dependencies which are required at compile time, but should not leak into runtime. This typically include dependencies which are shaded when found at runtime.                |
| runtimeOnly | Declaring runtime dependencies            |      no     |      no      | This is where you should declare dependencies which are only required at runtime, and not at compile time.                |
| testImplementation | Test dependencies    |      no     |      no      | This is where you should declare dependencies which are used to compile tests.                       |
| testCompileOnly | Declaring test compile only dependencies       |     yes     |      yes     | This is where you should declare dependencies which are only required at test compile time, but should not leak into the runtime. This typically includes dependencies which are shaded when found at runtime.                |
| testRuntimeOnly | Declaring test runtime dependencies       |      no     |      no      | This is where you should declare dependencies which are only required at test runtime, and not at test compile time                |

[Stackoverflow source](https://stackoverflow.com/questions/44493378/whats-the-difference-between-implementation-and-compile-in-gradle)
[https://docs.gradle.org](https://docs.gradle.org/current/userguide/java_library_plugin.html#sec:java_library_separation)

- The above Stackoverflow source also recommends `.aar` files to be added with `compileOnly` prefix. Will need additional tests on it.

- Though not tested, this library seems to configure API keys via `build.gradle` file, which is interesting given that most other libraries tend to do it via the Manfiest file.
```
android.defaultConfig.manifestPlaceholders=[
facebookAppId : "your facebook app id",
..
]
```

- For Google Auth, **Android OAuth** client needs to be created filling in the **SHA1** of the keystore and **package name**. This is a mandatory standard procedure for all Google authentication.

- Looks like the `disconnecting` part is also related to the main social app installed in the app. Eg. if Facebook app is installed, then this app will clear **active session only** on `disconnecting`, otherwise **clear all cookies** and then user willl have to relogin. This is interesting, given that I had faced similar issue related to **signing oug** of social account in some old projects.


- There is an additional feature for **revoking access**, which shows permission authorization page again when logging in, a feature that exists in Facebook and Google only.


- `git clone https://github.com/jaychang-917/SimpleAuth.git` !!

## [android-sociallogin](https://github.com/KosyanMedia/android-sociallogin) by [KosyanMedia](https://github.com/KosyanMedia)

- Requires `https://jitpack.io` to be added in repository, not exactly sure why. Maybe it is hosted in that url.
```
allprojects{
repositories {
maven { url 'https://jitpack.io'}
}
}
```
The library above it only required dependency to be added. Also this library, in compared to the one above it, has github link in the dependency url. Not sure if that makes any difference.

```
Social Login:
 compile 'com.github.KosyanMedia.android-sociallogin:sociallogin:x.y.z'

Simple Auth:
 compile 'com.jaychang:simpleauth:2.1.4'
```


- Both libraries so far have modularization. That is, an option to compile only, say Facebook login, and discarding everything else. This modularization, however, depends on a single core module as well.

```
compile 'some.core.module'
compile 'some.one.feature.module.say.facebook'
```

- The callback to the login module is via `onActivityResult(int requestCode, int resultCode, Intent Data);` which is neat considering I've already implemented in such a way.

- Also supports Rx Java

> RxJava is basically a Java VM implementation of ReactiveX, a library for composing asynchronous and event-based programs by using observable sequences. No much idea though. Needs more knowledge.<br>
Can be read [here](https://medium.com/@factoryhr/understanding-java-rxjava-for-beginners-5eacb8de12ca).

- `git clone https://github.com/KosyanMedia/android-sociallogin`!!




### [Social Login Helper for Android](https://github.com/mukeshsolanki/social-login-helper-Deprecated-) by [mukeshsolanki](https://github.com/mukeshsolanki)

- Deprecated but had this pretty nice logo from [shields.io](https://shields.io) or their [Github repo](https://github.com/badges/shields).

> I had seen such shields being used and turns out they serve a concise, consistent and legible badges for Github readmes and other web pages. 

Here's one showing ** stars ** for [Owncloud's Android App Repository](https://github.com/owncloud/android) : ![GitHub stars](https://img.shields.io/github/stars/owncloud/android?style=social)

- `git clone https://github.com/mukeshsolanki/social-login-helper-Deprecated- ` !

That is it! Now time to dive into coding! 
