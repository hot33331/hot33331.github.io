---
layout: post
title: How to NOT getting started with dotnet MAUI
description: Hiccups with the MAUI preview
img: dotnet-bot-surfing.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [dotnet, MAUI]
---

[.NET Multi-platform App UI (MAUI)](https://github.com/dotnet/maui) is now available in preview 5 and now really worth to give it a spin. 
Before you read any of my stuff, there is a very good [blogpost from David Ortinau](https://devblogs.microsoft.com/dotnet/announcing-net-maui-preview-5/) about current state and how to get startet.

I already did that and stumbled across some things that made my life harder, so I wrote them down, so that you don't have to suffer like I did:


## Trying to install on your own - DON'T!

One could be tempted to just install .net 6 preview from the website and get going. If you do that, there are some more things to take care of that are a bit tedious, so the nice Jonathan Dick (@redth) wrote an amazing tool called [maui-check](https://github.com/Redth/dotnet-maui-check) which makes your life a lot easier.

You can find the installation instructions on the readme.md in the github repo.
Unfortunately for me the problems already started, not being able to install that dotnet global tool.


## Using .net framework installed with homebrew - DON'T!

I don't know why, probably out of muscle memory, I had installed the .net framwork through brew. This seems to pose a problem though, hiding the SDKs that maui-check downloads.

You can read my cry for help here:

{::options parse_block_html="false" /}

<div class="center">

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Oh no - what am I doing wrong <a href="https://twitter.com/redth?ref_src=twsrc%5Etfw">@redth</a> ? :-o <a href="https://t.co/YNoM7VBv0L">pic.twitter.com/YNoM7VBv0L</a></p>&mdash; Tobias Hoppenthaler (@hot33331) <a href="https://twitter.com/hot33331/status/1387385922585567236?ref_src=twsrc%5Etfw">April 28, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

</div>

In the end I removed the brew instance of .net with

> brew uninstall --ignore-dependencies dotnet

and maui-check was able to download everything. Everything, well not quite, there was another problem...


## Multiple dotnet nuget sources - DON'T!

When I ran maui-check, I got the following output:

> /usr/local/share/dotnet/sdk/6.0.100-preview.4.21255.9/NuGet.targets(131,5): error : Failed to retrieve information about 'redth.net.maui.check' from remote source ...

This was due to the fact that I had multiple dotnet nuget sources configured and one of the sources caused this problem. After disabling all but https://api.nuget.org/v3/index.json with

> dotnet nuget disable source *sourcename*
  
This source also caused me troubles when doing the update of maui-check via
  
> dotnet tool update --global Redth.Net.Maui.Check
  
Error message was the same as above.


## Missing NuGet feed for MAUI

This should be fixed with preview 5 and I did not run into this problem anymore with p5 today, but before It seems that it was necessary to have a special local nuget.config. Read all about it in this tweet if you are a nostalgic:
 

{::options parse_block_html="false" /}

<div class="center">  
  
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">OOooops : <a href="https://twitter.com/hashtag/maui?src=hash&amp;ref_src=twsrc%5Etfw">#maui</a> is that on me?<br>Failed to check update for Microsoft.Maui.Templates::6.0.100-preview.4.634: the package is not available in configured NuGet feeds.</p>&mdash; Tobias Hoppenthaler (@hot33331) <a href="https://twitter.com/hot33331/status/1404346909783957504?ref_src=twsrc%5Etfw">June 14, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
  
</div>


## Build on Mac throws Windows errors
  
When I first built my app through the CLI on mac, I got this error:
  
> /usr/local/share/dotnet/sdk/6.0.100-preview.5.21302.13/Sdks/Microsoft.NET.Sdk/targets/Microsoft.NET.Sdk.FrameworkReferenceResolution.targets(64,5): error NETSDK1100: Windows is required to build Windows desktop applications. [/Users/hot33331/Projects/MauiFive/MauiFive.WinUI/MauiFive.WinUI.csproj]

My way of solving this was to delete the WinUI folder, since I would not need that on mac, anyways for now:

> rm -R MauiFive.WinUI/

And also remove the project from the .sln :

> Project("{9A19103F-16F7-4668-BE54-9A1E7A4F7556}") = "MauiFive.WinUI", "MauiFive.WinUI\MauiFive.WinUI.csproj", "{04594CAA-9E35-4049-8B08-A5C9348D2114}"
EndProject

After that I was able to run the build

> dotnet build -t:Run -f net6.0-maccatalyst


## Docs

Fresh from the oven: WE HAVE DOCS!

https://docs.microsoft.com/en-us/dotnet/maui/

Thanks to David Britch!


And with that I hope this helps you getting started with MAUI, I am more than thrilled for the things to come and will continue tinkering with the previews.






