# React Native RICOH THETA Demo Installation Guide for Windows

![react-windows-header](images/react_native/windows/reactwindows.svg)

## Overview

This section covers the installation process for React Native on **Windows 11** so that we can run the `demo-react-native`. 
Another section will cover the installation for macOS. 

For this installation you will need to install **Node.js** if you haven't already. 

There will be videos and links in the resource section for the installation of node.js on your computer. This article also covers how to build the `theta-client` and make it available to `demo-react-native`, as well as building the `demo-react-native` and running it on an Android emulator. 

The results will be shown using the **THETA X** running the `demo-react-native`  using the THETA API.

## General Steps to run React Native Demo on Windows

1. Build the `theta-client` and make it available to `demo-react-native`
2. Build `demo-react-native`
3. Test the `demo-react-native` build on **THETA X** with an emulator
4. Test all demo features: List Files, Take Photo

Resources

* [GITHUB React Native demo for theta-client](https://github.com/ricohapi/theta-client/tree/main/demos/demo-react-native)

* [VIDEO theta-client React Native full build tutorial and demonstration](https://www.youtube.com/watch?v=SqzDomDikcM)

* [VIDEO HowTo Install nvm, node, npm and yarn on Windows 11](https://www.youtube.com/watch?v=NWUfaXFPv50)

## Work Environment

| Dell XPS 13 | Details                              |
| ----------- | ------------------------------------ |
| CPU         | Intel(R) Core(TM) i7-10710U CPU @ 1.10GHz   1.61 GHz  |
| RAM         | 16.0 GB |
| OS          | Windows 11 Home |

THETA X running firmware 1.41.0

# React Native install on Windows

## Requirements
[Android Studio](https://developer.android.com/studio)


## Command Line Steps

First Command - Clone the Repo with `git clone https://github.com/ricohapi/theta-client.git`
![firstCommand](images/react_native/gitCloneThetaClient.png)

Second Command -  Go into  **theta-client** directory with `cd theta-client`
![secondCommand](images/react_native/cdThetaClient1.png)

Third Command - Build Gradlew with `./gradlew publishToMavenLocal podPublishXCFramework` but I have an Error, the problem is the SDK location is not found. My solution is to set the environment variable of the SDK.
![thirdCommand](images/react_native/gradleWPublishFail.png)

## Steps to Fix for Build Failure:

1.  Search for env

    ![envVarScrenshot](images/react_native/envVar.png)

2.  Click on environmental variables

    ![pressOnEnv](images/react_native/envVarPress.png)

3.  New System Variable

    ![newEnvVar](images/react_native/newEnvVar.png)

4.  Type in the Variable name `ANDROID_HOME` and set the path `C:\Users\UserName\AppData\Local\Android\Sdk`

    ![settingPathScreenshot](images/react_native/settingEnvVar.png)


By default the path to the SDK usually is `C:\Users\UserName\AppData\Local\Android\Sdk` , Copy the Path substituting for your `UserName` 

![pathscreenshot](images/react_native/pathScreenshot.png)


5.  Restart your terminal by closing and relaunching it before trying out the `gradlew` build command again


## Command Line Steps Continued

Retry Third Command - Try the Build Gradlew command again `./gradlew publishToMavenLocal podPublishXCFramework`

![tryAgainScreenshot](images/react_native/retryGradle.png)

Screenshot below shows its successful
![successScreenshot](images/react_native/successBuild.png)

Fifth Command - Set the environment variable of THETA_CLIENT with the process shown above using the Windows Environment Variable Editor. 

`Variable Name : THETA_CLIENT`

`Variable Path : C:\Users\Erik Rodriguez\Projects\theta-client`

Substitute the variable path for your local path to `theta-client`

![exportVarScreenshot](images/react_native/exportVar.png)

Check if it sucessfully set the variable with `echo $Env:THETA_CLIENT` it should return the path of the THETA_CLIENT variable if set correctly

![correctPath](images/react_native/checkPath.png)


Sixth Command - Go into **react-native** directory with `cd react-native`

![cdReactNative](images/react_native/cdreactnative.png)

Seventh Command - run `bash ./mkpackage.sh` and as it appears we have errors to fix

![bashCommand](images/react_native/bashcommand.png)

To fix the mkpackage error:

1. Open up the VSCode editor, install it if you don't have it

2. Open the file called `mkpackage.sh` in the `theta-client\react-native` directory

3. Convert the `mkpackage.sh` file `CRLF` to `LF` by clicking on the bottom right `CRLF` button and changing it to `LF` as shown

![convertFile](images/react_native/convertFile.png)

4. Save the file by pressing `ctrl-s` and you should be good to go!

Retry Seventh Command - run `bash ./mkpackage.sh`

![bashGood](images/react_native/bashsuccesful.png)

Go into the `demo-react-native` folder as shown below from the root directory `theta-client`

    cd demos
    cd demo-react-native
![Alt text](images/react_native/goIntodemo.png)

Once you are in `theta-client\demos\demo-react-native`

Eigth command - run `yarn install` if you dont have yarn downloaded on your computer already then you need to get it by running 

![errorYarn](images/react_native/yarninstallerror.png)