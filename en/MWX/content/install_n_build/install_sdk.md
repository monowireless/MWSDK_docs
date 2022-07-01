---
title: "Installing the TWELITE SDK"
author: "Mono Wireless Inc."
description: "Installing the TWELITE SDK"
---
# Installing the TWELITE SDK

{% hint style="success" %}
The following description corresponds to TWELITE STAGE SDK MWSDK2020\_12 or later
{% endhint %}

{% hint style="info" %}
If you have downloaded the TWELITE STAGE SDK, extract the distribution zip archive to a directory that **does not contain Japanese or whitespace characters.**

See also about TWELITE STAGE:

[Install, usage](https://mono-wireless.com/jp/products/stage)

[Supplemental information about installation](https://stage.twelite.info)
{% endhint %}

### 3. set environmental variable

{% hint style="warning" %}
If you are using the TWELITE STAGE application, you <mark style="color:red;">**do not need**</mark> <mark style="color:red;"></mark><mark style="color:red;"></mark> to set any environment variables. If you want to build with the command line, please set them.
{% endhint %}



`MWSDK_ROOT`, `MWSDK_ROOT_WINNAME`(for Windows10) need to be set.

#### Windows10,11
In this example, the name of the extracted directory is `C:\MWSTAGE`. If you have installed the software in a different directory, please change the name.

Run `C:\MWSTAGE\Tools\SET_ENV.CMD` to set the following environment variables:

* `MWSDK_ROOT`
* `MWSDK_ROOT_WINNAME`

For example, the following variables are set:

```
MWSDK_ROOT=C:/MWSTAGE/MWSDK/
MW_ROOT_WINNAME=C:\MWSTAGE\MWSDK\
```


{% hint style="warning" %}
To uninstall the TWELITE STAGE SDK from the installed PC, please do the following:

* Run `UNSET_ENV.cmd`. This will unset the environment variables.
* Delete the MWSTAGE directory.
{% endhint %}

#### Linux
Set the development environment and shell to reflect the MWX\_ROOT environment variable.

There are several ways to do this, but add the following setting to the `.profile` of your home directory (if the file does not exist, please create a new one). You can even build VSCode with this setting.

`MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK/`\
`export MWSDK_ROOT`



To add it without using the editor, enter the command as follows. The $ is a prompt and will be displayed differently depending on your environment. The `/foo/bar/MSWSDK` part should be rewritten according to the installed directory.

```bash
$ cd $HOME
$ echo MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK>>.profile
$ echo export MWSDK_ROOT>>.profile
```

#### macOS
Set the development environment and shell to reflect the `MWX_ROOT` environment variable.



There are several ways to do this, but add the following settings to `.profile` in your home directory (create a new file if you don't have one). You can even build VSCode with this setting.

`MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK/`\
`export MWSDK_ROOT`



To add it without using the editor, enter the command as follows. The $ is a prompt and will be displayed differently depending on your environment. The `/foo/bar/MSWSDK` part should be rewritten according to the installed directory.

```bash
$ cd $HOME
$ echo MWSDK_ROOT=/foo/bar/MWSTAGE/MWSDK>>.profile
$ echo export MWSDK_ROOT>>.profile
```


{% hint style="info" %}
Use LaunchD to apply `MWSDK_ROOT` to the entire environment.

Some settings in VS Code refer to environment variables, but they are not required for the build.
{% endhint %}

### 4. Applying library fixes

The library resource code may have been modified since the time it was included in the SDK. Please refer to the [revision history](../revisions.md) and replace the library resource code as necessary.



