---
layout: post
title: XF5 breaks build
description: 'Updating to Xamarin Forms 5 broke my build :-o'
img: xf5.png
fig-caption: null
tags:
  - Xamarin
  - Xamarin.Forms
published: true
---

I recently updated an app to Xamarin.Forms 5 and after that I got the following errors at compile time:

> FileName.xaml: Value cannot be null. Parameter name: method

The same code compiled and worked fine before with Xamarin.Forms 4. After some googling and asking the one and only Gerald V. I found this:

[https://github.com/xamarin/Xamarin.Forms/issues/4678](https://github.com/xamarin/Xamarin.Forms/issues/4678)

After some digging I tried removing the Xaml precompile flags from my pages' code behind files:

> [XamlCompilation(XamlCompilationOptions.Compile)]

This did the trick for me.

UPDATE: it seems that if this happens, you need a direct dependency to the respective Xamarin Forms 5 nuget from the project you are getting this error. If you add that direct dependency, the errors should go away, too while maintaining the Xaml Compilation.
