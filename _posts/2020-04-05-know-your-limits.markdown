---
layout: post
title: Know your limits - app size limits and how to overcome them
date: 2020-04-05 07:27:00 +0100
description: App size restrictions and how to overcome them. # Add post description (optional)
img: speed_limit.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Xamarin,Android,iOS,AppSize,Store]
---
Most of you might never get into the position where app size limits matter to you. Apps should be small and do one thing well and one thing only. But for games or other heavy ressource apps, you might hit those limits. Since Xamarin already addes some extra weight to your app, you might hit those limits sooner than with native development.


## Know your limits
For Google Play Store the size limit is pretty low: at only [100MB](https://developer.android.com/google/play/expansion-files) you're done while Apple allows you [4GB](https://developer.apple.com/news/?id=02122015a) app size in the store. This is pretty generous, but users per default have a size limit of [100MB](https://developer.apple.com/news/?id=02122015a) for download via cellular which you should keep in mind.


## How to reduce your app size
There are different approaches to this topic for the oses.


### Android
https://developer.android.com/topic/performance/reduce-apk-size


### iOS
https://developer.apple.com/documentation/xcode/reducing_your_app_s_size


## Cannot reduce size - what now?
Well if you for the love of it cannot cut down on app size, there are ways to get around that.


### Load resources from a backend
This works for all platforms. You can just download your resources when your app starts the first time, or lazy whenever you need them. 


### Android App Bundles
Android App Bundles is the new way of trimming down your app. It is powered by the play store, knowing your users device and locale and therefore creating an apk specifically to its needs. Images are only downloaded for your devices's resolution and language files only for your language. Using App bundles also gives you the added benefit that your app can now have up to 150 MB.
https://developer.android.com/topic/performance/reduce-apk-size#app_bundle


### Android expansion files
https://stackoverflow.com/questions/12371302/android-apk-size-limitation-in-google-play
https://developer.android.com/google/play/expansion-files
