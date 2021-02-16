---
layout: post
title: Xamarin Forms everywhere
date: 2021-01-22 09:27:00 +0100
description: Xamarin Forms on all platforms
img: xamicon.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Xamarin]
---
Xamarin Forms is multiplatform with as much code-reuse as possible. I worked quite some time with iOS and android, but never had set foot to other platforms, so I wanted to see how well Xamarin Forms works out of the box on other platforms with the focus on desktop.

I wanted to cover 
* iOS
* Android
* Windows (UWP/WPF)
* Linux (GTK)
* macOS ("standard" and Frank Kruger's Catalyst version)

I used the Vs4mac Template for multiplatform app with flyout, non-shell. I updated everything to the latest Xamarin Forms and Essentials.

I documented my efforts in a github repo: [https://github.com/hot33331/XamarinFormsEverywhere](https://github.com/hot33331/XamarinFormsEverywhere)


## iOS
As expected iOS works great, no hiccups, everything is fine.

![iOS screenshot](../assets/img/xf_ios.png)

## android
See iOS.

![iOS screenshot](../assets/img/xf_android.png)

## Windows
Now this is where things get interesting. UWP runs okay if you know that you have to click on the dots in the upper right to get the menu for adding things.

![uwp1 screenshot](../assets/img/uwp1.png)

![uwp2 screenshot](../assets/img/uwp2.png)

![uwp3 screenshot](../assets/img/uwp3.png)

WPF does not show any items or the flyout. However if you click around in the white space you might manage to popuot that flyout (see second screenshot).

![wpf1 screenshot](../assets/img/wpf_empty.png)

![wpf2 screenshot](../assets/img/wpf_flyout.png)


## Linux
You can develop easily from your mac for GTK (gets installed with Visual Studio) and run that same code on Linux (I testet on Ubuntu with Mono Develop IDE - you could also use [jetbrains Rider](https://www.jetbrains.com/rider/) on Linux). Unfortunately it also does not seem to be very mature, yet and does not show any items.

![gtk1 screenshot](../assets/img/gtk1.png)

Clicking around in the white space also reveals the flyout as in WPF.

![gtk2 screenshot](../assets/img/gtk2.png)

## macOS
While the "out-of-the-box" project does have some hiccups: not showing items and action button.

![macOS screenshot](../assets/img/xf_macos.png)

The catalyst version (using [Frank Krugers nuget](https://github.com/praeclarum/Praeclarum.MacCatalyst)) works flawless and snappy:

![macCatalyst screenshot](../assets/img/xf_catalyst.png)

but it is still in alpha state and if I remember correctly apps cannot be signed for the app store, just yet. 


# Conclusion
I was pretty disappointed by the desktop implementations. I had the expectation that the basic file - new - template would work at least. Unfortunately only UWP worked with one minor complaint. I have high hopes that the support for desktop will get better with .net 6 and MAUI since I think I remember from some of David Ortinau's slides that Windows (WinUI3 in the future) and macOs (hopefully Frank's catalyst version) will be supported by Microsoft. From my point of view the current state of Desktop (maybe with exception of UWP) in Xamarin Forms 5 is not ready for production use, yet.

P.S. I found some proof for my earlier claims in one of the [videos from .net Frontend Day](https://www.youtube.com/watch?v=RnyZZKjdUxk).

![mssupport screenshot](../assets/img/ms_support_desktop.PNG)

![winui3_catalyst screenshot](../assets/img/winui3_catalyst.PNG)



