# Dynamic Analysis

Install an application

```sh
adb install apkfile.apk
```

Intercept application traffic with Burp Suite and install a trusted certificate authority at the Android OS level

```sh
openssl x509 -inform PEM -subject_hash -in BurpCA.pem | head -1
cat BurpCA.pem > 9a5ba580.0
openssl x509 -inform PEM -text -in BurpCA.pem -out /dev/null >> 9a5ba580.0
adb root
abd remount
adb push 9a5ba580.0 /system/etc/security/cacerts/
adb shell "chmod 644 /system/etc/security/cacerts/9a5ba580.0"
adb shell "reboot"
```

- **PID Cat**

Tool to display log entries for a specific application package when `debug=true` is enabled in the application.

## Drozer

It is a complete security audit and attack framework for Android.
The prerequisite is that you have Drozer installed on your computer and the Drozer agent on your emulator or devices.

Connect

```sh
adb forward tcp:31415 tcp:31415
drozer console connect
```

Get package information

```sh
run app.package.list

run app.package.info -a
```

Identify the attack surface, unprotected activities and more

```sh
run app.package.attacksurface package_name 
```

See which activities can be exploited.

```sh
run app.activity.info -f package_name
```

Start unprotected activities!

```sh
run app.activity.start --component package name component_name
```


