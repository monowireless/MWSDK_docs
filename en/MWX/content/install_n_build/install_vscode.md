---
title: "Installing VS Code"
author: "Mono Wireless Inc."
description: "Installing VS Code"
---

# Installing VS Code

VisualStudio Code (VS Code) is recommended to make Act (source code) writing easier. The attached Act contains a file that has been configured to ensure that the code is interpreted properly in VS Code.

{% hint style="warning" %}
VS Code reads source files and header files and interprets the source code, thus providing function definition information and function and method name completion to help you write source code. The MWX library requires more header files to be loaded than the C library. In comparison to C development, the MWX library requires more header files to be loaded and the editor may be slower in some environments.
{% endhint %}



## Installing VSCode

{% hint style="danger" %}
Please note that this support does not cover questions about how to install or use VSCode. Please refer to the information available in the public domain.

Depending on your environment, you may need to configure security settings or other settings in order to install the software. Please check with your system administrator whether installation is possible, and refer to the distributor or general information for instructions.
{% endhint %}

VSCode allows you to do the following:

* Editing the source code
* Connection to GIT (if you do your own source control on GIT)
* The IntelliSense based on source code interpretation (\*not all definitions can be guaranteed to be interpreted correctly)



VSCode can be downloaded from the link below.

{% embed url="https://code.visualstudio.com" %}

###

### Installing plug-ins

To enable Visual Studio Code to interpret C/C++ language descriptions, install a plugin.

* C/C++ for Visual Studio Code



## Notes

{% hint style="warning" %}
The MWX library examples include a `.vscode` definition. This definition uses the MWSDK\_ROOT environment variable to identify the source code of the library (under `{MWSDK_ROOT}/TWENET/current`).

When launching VSCode from TWELITE STAGE, those settings such as `MWSDK_ROOT` will be setup automatically. In some cases, such as when you have already started VSCode, the settings may not be reflected.
{% endhint %}

{% hint style="warning" %}
VS Code's interpretation of source code is not always the same as the compiler's interpretation. Also, depending on how the source code is edited, the interpretation may be more incomplete.&#x20;
{% endhint %}
