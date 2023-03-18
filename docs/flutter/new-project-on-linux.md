# New Flutter Android Project on Linux

Using theta-client v1.0.0.

## create new project

```text
flutter create --platforms=android -a kotlin theta_mini
Creating project theta_mini...
cd theta_mini/
mkdir packages
mkdir packages/theta_client_flutter
```

## copy theta-client package

![copy theta-client plugin](../images/flutter/linux/copy_flutter_plugin.png)

## add theta-client to android

In `packages/theta_client_flutter/android/aar`, copy the `.aar` files
that were built in the theta-client package build step.

`theta-client/kotlin-multiplatform/build/outputs`

![copy aar files](../images/flutter/linux/copy_aar.png)


## configure Flutter

In `pubspec.yaml`, add the theta-client package as a dependency.

```yaml
dependencies:
  flutter:
    sdk: flutter
  theta_client_flutter:
    path: ./packages/theta_client_flutter
```

## configure Android build

In `android/app/build.gradle`, make the following changes.

```groovy
if (flutterRoot == null) {
    throw new FileNotFoundException("Flutter not found. Add flutter.sdk in local.properties.")
}
...
...
defaultConfig {
    applicationId "com.oppkey.theta_mini"
    minSdkVersion 26
dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    implementation files('../../packages/theta_client_flutter/android/aar/theta-client-debug.aar')    
}    
```
