+++
title = "Android Emulation for Expo apps"
date = 2026-01-27
authors=["Violet Chan"]
draft = false
+++

We made the decision to build the client app for Volery in React.js using the Expo framework. Expo comes bundled with the ability to build a version of the app to be used on a real phone via the Expo app or to be emulated via an SDK integration. We decided to use Android Studio's built in SDK and emulator tools with Express. 

While trying to take advantage of this convenient integration, we ran into a bunch of pit falls that took days of trouble shooting.

For one, my development machine is a lightweight laptop -- a fact that doesn't normally matter but the fact that Expo needs the emulator running while it builds the app means that my CPU can quickly get throttled if it's running any other intensive processes. So unfortunately during troubleshooting, having remote assistance helped with figuring out what to do, but also got in the way of the machine being able to do it. If you're also having problems running Expo with Android Studio, keep that in mind if you are trying to test the client on your own machine.

The next thing to try, is cold booting the emulator from Android Studio rather than letting Expo start it. Some times the first boot of the emulator can hang, and rebooting it helps, you may alsop need to clear any cached data before rebooting the emulator. For whatever reason, Android Debug Bridge can have trouble detecting the process if not started from the Studio interface. The fact that ADB wasn't detecting the emulator took us a while to figure out and fixing the issue took longer, because there were a couple other things to take care of first. 

On my machine, despite fresh installing everything, some ADB files had to be manually created or renamed. If you get an error relating to the Android Debug Bridge saying that it cannot find a certain file or directory, try creating an empty file/directory with the proper name. Otherwise you may need to move the location of the ADB apk (see [this github issue](https://github.com/facebook/react-native/issues/18243)). Essentially we need to use an ADB command to install the APK where Expo expects it.

I mentioned earlier that some problems were caused by the amount of resources that building the app and emulating a phone take. By default the Android emulator's heap allocation was too small, which meant it was prone to freezing. I initially tried to rectify the issue by tripling the amount of allocated heap memory. That didn't actually improve performance much, I suspect because the emulator was now causing performance issues for my computer or the build process. Either way the emulator was prone to freezing and the build process would hang or fail, or the machine itself would crash. 512Mb of heap seems to be the sweet spot.

There were also some issues with pathing. My original solution was to try again in an Ubuntu VM on a more powerful windows machine, but making sure that Expo and Android studio were both accessing the correct versions of all the packages and not trying to use Windows packages instead was more trouble than it was worth.