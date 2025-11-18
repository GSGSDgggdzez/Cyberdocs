# Reversing

Extract the apk from the device and get the source code.

## Initialization

View connected devices

```sh
adb devices
```

Interact with the device

```sh
adb shell
```

## Extract apk to analyze

For this, you need to have installed the application on your device and know the package name.

List installed applications.
This command prints the path to the APK of the given file

```sh
adb shell pm list packages
```

Get the path of an application (the path to the APK file)

```sh
adb shell pm path <PACKAGE_NAME>
```

Download the APK

```sh
adb pull <PACKAGE_NAME>.apk NEW_APP_NAME.apk
```

## Get the source code

Allows you to simply load an APK and view its Java source code. In fact Jadx decompiles the APK to smali, then converts the smali back to Java.

```sh
jadx -d destination-folder path-apkfile.apk
# or
jadx -d destination-folder path-dexfile.dex
```

Convert an APK to a JAR file. Then open the `JAR` file with `JD-GUI` to get the Java code.

```sh
d2j-dex2jar file.apk 
```

Get the source code in smali.

```sh
apktool d file.apk
```
