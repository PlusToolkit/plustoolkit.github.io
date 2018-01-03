---
layout: page
title: Developer's guide
group: navigation
order: 5
description: ""
---
{% include JB/setup %}

Source code
-----------

Plus toolkit contains three main repositories:
- [PlusLib](https://github.com/PlusToolkit/PlusLib/): Library that contains all data acquisition and processing implementation. It contains a few sipmle tools and test applications but primarily intended to be linked into software applications.
- [PlusApp](https://github.com/PlusToolkit/PlusApp/): Software applications with graphical user interface that use PlusLib to make features available to end users.
- [PlusBuild](https://github.com/PlusToolkit/PlusBuild/): Small project that downloads and builds PlusLib, PlusApp and all their dependencies (VTK, ITK, etc.).

Documentation
-----------------

- <a href="http://perk-software.cs.queensu.ca/plus/doc/nightly/dev/">PlusLib API documentation</a>: generated nightly from the latest code version.
- [Plus devices](https://github.com/PlusToolkit/PlusBuild/blob/master/devicecode.md): description of the steps requires to implement a new device interface.

Testing dashboards
------------------

- [PlusLib dashboard](http://perkdata.cs.queensu.ca/CDash/index.php?project=PlusLib): results of automatic tests of the Plus library
- [PlusApp dashboard](http://perkdata.cs.queensu.ca/CDash/index.php?project=PlusApp): results of automatic tests of the Plus applications

Build instructions
------------------

Plus library files and all required libraries and toolkits are automatically downloaded, configured, and built using CMake "superbuild" method (using CMake external project infrastructure). Build instructions are available in [PlusBuild repository](https://github.com/PlusToolkit/PlusBuild/blob/master/README.md).

Supported platforms:
- 32/64-bit builds: Plus can be built in either 32-bit or 64-bit mode. 64-bit applications have the advantage of larger available memory space (which is useful for certain applications, such as recording a large number of frames in memory, or reconstructing high-resolution volumes), but only a few hardware devices have 64-bit compatible drivers. If available memory is not a concern &nbsp;then use only 32-bit builds. If lots of memory is needed, and the application does not have to use tracking or imaging hardware devices directly then 64-bit build of Plus can be used. If both hardware support and lots of memory is needed then a 32-bit build of Plus can be used for data acquisition and the acquired data can be passed on to a 64-bit Plus or other application for further processing.
- Windows 7 32-bit/64-bit, Windows 10 32-bit/64-bit, Windows XP 32-bit embedded, Ubuntu 16.04, and MacOSX operating systems are fully supported and regularly tested.
- Running on Linux and MacOS: Unfortunately, many of the drivers written for devices are Windows specific, and thus capture cannot be done on a Linux or MacOSX machine. It is recommended to do the data acquisition on Windows and stream the acquired data to the Linux or MacOS computer for further processing.

Contributing
----------

We follow the standard [GitHub Flow](https://guides.github.com/introduction/flow/) process. In short: send a pull request with proposed changes. See more information [here](https://github.com/PlusToolkit/PlusBuild/blob/master/CONTRIBUTING.md).

When making code changes, please follow Plus coding conventions. The Astyle formatter can be used to quickly format a file to Plus standards.
* PLUS format:
  * --style=allman
  * --indent=spaces=2
  * --align-pointer=type
  * --indent-namespaces
  * --indent-col1-comments
  * --pad-oper
  * --unpad-paren
  * --add-brackets
  * --add-one-line-brackets
  * --keep-one-line-blocks
  * --convert-tabs
  * --mode=c

