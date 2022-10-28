# Build After Effects Plugin(.aex) with CMake

This repository contains instructions for building Adobe After Effects plugins using CMake.

## Details
Plug-ins in other software used in the studio can be produced using CMake; the AfterEffects SDK samples rely on Visual
Studio, which we wanted to replace with CMake.
Then I found a page on the Internet where people were actually working on building with CMake.
I was able to learn how to process mainly PiPL.r files. We will continue to update it to serve as a template for
creating plug-ins in CMake.

## Requirements
What I have described here is the environment I tested.

* After Effects 2023 (23.0)
* CLion 2022.2.4
* CMake 3.25.0-rc2
* Visual Studio 2022 17.3.6
* MSVC v143

## Acknowledgments

The following link is to one of the few who used the CMake approach to AEX found on the Internet.
We would like to give a big thanks to the creators.

* [Github - Wunkolo / Vulkanator](https://github.com/Wunkolo/Vulkanator)
* [Github - Gorialis / aftereffects_spatial_media_plugins](https://github.com/Gorialis/aftereffects_spatial_media_plugins)
* [使用CLion开发After Effects插件](https://idom.me/articles/851.html)
* [Adobe Support Community - Any examples for building AE plugins on OSx with cmake?](https://community.adobe.com/t5/after-effects-discussions/any-examples-for-building-ae-plugins-on-osx-with-cmake/m-p/8399527)