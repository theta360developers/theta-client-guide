# Community Guide for theta-client

![tablet](images/tablet.png)

Full code on  [GitHub ricohapi/theta-client](https://github.com/ricohapi/theta-client).

## Quickstart

For native Android and iOS

1. Build `theta-client` first
2. Copy `aar` file you built in the previous step into Android project
3. Copy `XCFramework` into iOS project
4. In `./demo/demo-android` build Android demo
5. In `./demo/demo-ios` build iOS demo

* [demo-android full build process video walkthrough](https://youtu.be/l8X6amOmHXI)


## Overview

`theta-client` is an open source library enabling rapid creation of mobile apps that control RICOH THETA cameras. The library works with Kotlin, Swift, Dart, and JavaScript.

## Demo Apps

Four open source demo applications are included:

* [Android native with Kotlin](https://github.com/ricohapi/theta-client/tree/main/demos/demo-android)
* [iOS native with Swift](https://github.com/ricohapi/theta-client/tree/main/demos/demo-ios)
* [React Native for iOS and Android builds](https://github.com/ricohapi/theta-client/tree/main/demos/demo-react-native)
* [Flutter for iOS and Android builds](https://github.com/ricohapi/theta-client/tree/main/demos/demo-flutter)

## Documentation

Refer to theta-client documentation for the development platform you are using.

* [Android](https://github.com/ricohapi/theta-client/blob/main/docs/tutorial-android.md)
* [iOS](https://github.com/ricohapi/theta-client/blob/main/docs/tutorial-ios.md)
* [React Native](https://github.com/ricohapi/theta-client/blob/main/docs/tutorial-react-native.md)
* [Flutter](https://github.com/ricohapi/theta-client/blob/main/docs/tutorial-flutter.md)

In addition to documentation on theta-client, you can refer to the
RICOH official [Web API 2.1 documentation](https://github.com/ricohapi/theta-api-specs/tree/main/theta-web-api-v2.1).


## Community Tips

### cannot find ANDROID_HOME (Android)

You may need to specify the path of ANDROID_HOME in either an
environmental variable or the `local.properties` file in the
project root.

Example `local.properties` on Linux.

`sdk.dir=/home/craig/Android/Sdk`

### zip END header not found (Android)

After you build theta-client, make sure that you copied
`theta-client-debug.aar` into `theta-client\demos\demo-android\app\libs`

### React Native: run pod install in ios folder

For React Native, you may need to run `pod install` in the ios 
folder inside of demo-react-native

### Change Equirectangular Image to 360 Navigation View (Flutter)

Oppkey uses [panorama](https://pub.dev/packages/panorama).

[video tutorial](https://youtu.be/9hWUU6G3Ank)

After taking a picture, the post-view is also in equirectangular.

![post view](images/windows_flutter/postview.png)


Add Panorama package.

```text

PS C:theta-client\demos\demo-flutter> flutter pub add panorama
Resolving dependencies...
```
Your dependencies will look like this:

```yaml
dependencies:
  flutter:
    sdk: flutter
  theta_client_flutter:
    path: ./packages/theta_client_flutter


  # The following adds the Cupertino Icons font to your application.
  # Use with the CupertinoIcons class for iOS style icons.
  cupertino_icons: ^1.0.2
  video_player: ^2.4.10
  panorama: ^0.4.1
```

In `lib/photo_screen.dart`, go to line 19 and wrap with Panorama.

![wrap with widget lightbulb](images/windows_flutter/lightbulb.png)

![wrap with widget](images/windows_flutter/wrap_with_widget.png)

If you don't have auto-import, the `Panorama` widget will initially
be red.

![panorama red](images/windows_flutter/panorama_red.png)

On VS Code, use ctrl-. to open up the auto-import menu.  

![panorama import](images/windows_flutter/panorama_import.png)

Hot restart

Select a file from list view.

![list files](images/windows_flutter/list_files.png)

View in 360.

![360 view](images/windows_flutter/360_view.png)

### Build Flutter on Windows for Android

After building `theta-client`, inspect `theta-client/scripts/build-flutter-build.sh`

The key part is:

`cp -f ./kotlin-multiplatform/build/outputs/aar/*.aar ./flutter/android/aar/`

On PowerShell, copy the `*.aar` files into `./flutter/android/aar`

```
PS C:theta-client> copy .\kotlin-multiplatform\build\outputs\aar\*.aar .\flutter\android\aar\
PS C:theta-client> cd .\flutter\android\aar\
PS C:theta-client\flutter\android\aar> ls

    Directory: C:\Users\craig\Documents\Development\ricoh\2023\theta-client\flutter\android\aar


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----         2/24/2023  12:38 PM              0 .gitkeep
-a----         2/24/2023  12:40 PM         954368 theta-client-debug.aar
-a----         2/24/2023  12:40 PM         906203 theta-client-release.aar
```

In `demo-flutter\packages`, delete the file `theta_client_flutter` and replace
with a new folder called `theta_client_flutter`

![theta_client_flutter file](images/windows_flutter/theta_client_flutter_file.png)

Copy the contents `.\flutter` into the new `theta_client_flutter` folder.

![theta_client_flutter package](images/windows_flutter/theta_client_flutter_package.png)

In `demo-flutter`, run `flutter pub get`

```
PS C:theta-client\demos\demo-flutter> flutter pub get
Running "flutter pub get" in demo-flutter...
Resolving dependencies... (1.1s)
> async 2.10.0 (was 2.9.0)
> boolean_selector 2.1.1 (was 2.1.0)
  characters 1.2.1 (1.3.0 available)
> collection 1.17.0 (was 1.16.0) (1.17.1 available)
> js 0.6.5 (was 0.6.4) (0.6.7 available)
> matcher 0.12.13 (was 0.12.12) (0.12.14 available)
> material_color_utilities 0.2.0 (was 0.1.5)
  meta 1.8.0 (1.9.0 available)
  path 1.8.2 (1.8.3 available)
  plugin_platform_interface 2.1.3 (2.1.4 available)
> source_span 1.9.1 (was 1.9.0)
> stack_trace 1.11.0 (was 1.10.0)
> stream_channel 2.1.1 (was 2.1.0)
> string_scanner 1.2.0 (was 1.1.1)
> test_api 0.4.16 (was 0.4.12) (0.4.18 available)
> vector_math 2.1.4 (was 2.1.2)
  video_player 2.4.10 (2.5.2 available)
  video_player_android 2.3.10 (2.3.11 available)
  video_player_avfoundation 2.3.8 (2.3.9 available)
  video_player_platform_interface 6.0.1 (6.0.2 available)
  video_player_web 2.0.13 (2.0.14 available)
Changed 12 dependencies!
PS C:theta-client\demos\demo-flutter>
```

Start an Android emulator.

Run the Flutter application on the emulator.

```
PS C:theta-client\demos\demo-flutter> flutter run -d emulator-5554
Launching lib\main.dart on sdk gphone64 x86 64 in debug mode...
Running Gradle task 'assembleDebug'...                             80.8s
✓  Built build\app\outputs\flutter-apk\app-debug.apk.
Installing build\app\outputs\flutter-apk\app-debug.apk...        2,451ms
Syncing files to device sdk gphone64 x86 64...                     172ms
...
💪 Running with sound null safety 💪
```

Unless your computer is already connected to a RICOH THETA
camera, you will see _Initialize error_.  

![initialize error](images/windows_flutter/initialize_error.png)

Connect Windows computer to camera.

![connect](images/windows_flutter/connect.png)

![flutter example connection](images/windows_flutter/flutter_example.png)

After pressing take picture, the live preview will appear.

![live preview](images/windows_flutter/live_preview.png)




## Getting Help

Open an [issue on GitHub](https://github.com/ricohapi/theta-client/issues). 


