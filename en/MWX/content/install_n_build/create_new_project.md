---
title: "Creating a new project"
author: "Mono Wireless Inc."
description: "Creating a new project"
---
# Creating a new project

To create a new project, copy the folder of an already existing sample act with a different name and edit the file name.

{% hint style="warning" %}
The destination folder does not have to be a folder under the MWSDK. However, the folder name **must not contain any whitespace characters or Japanese names**.

Some workspace definitions in VS Code will not work if copied to a folder other than MWSDK. If you have added the source code folder for the mwx library to your workspace, please set it up anew.

There is no effect on the build without the library source setting. This setting is for deeper code interpretation on VSCode and to improve editing efficiency.
{% endhint %}



The file structure of the project is as follows (we'll use `PingPong` as an example)

```
Act_samples
  +-PingPong
    +-PingPong.cpp   : ACT file
    +-build          : build dir
    +-.vscode        : setting fils for VSCode    
```

Copy this `PingPong` folder to another location (but without Japanese characters or spaces in the folder name).

```
SomeDir
  +-AlphaBravo
    +-PingPong.cpp -> AplhaBravo.cpp (Note: Changed file name)
    +-build          : build dir
    +-.vscode        : setting files for VSCode
```

The only thing you need to edit is the file name `PingPong.cpp`. Change it to `AlphaBravo.cpp`, the same as the folder name.

{% hint style="success" %}
Run `build\build-BLUE.cmd` and if a BIN file is generated, it' is done (Windows 10).

On Linux/macOS, run `make TWELITE=BLUE` to see if the build succeeds.
{% endhint %}



{% hint style="info" %}
* ~~A .cpp file with the same name as the project folder name is mandatory.~~ (As of MWSDK 2020-04, arbitrary file names are now allowed)
* To add a file to be built, edit build/Makefile. See the Makefile documentation for instructions on how to edit it.
{% endhint %}

