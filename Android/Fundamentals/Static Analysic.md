# Static Analysis

Done without running the program, what will we identify?

- Weak or inappropriate use of cryptography
- Exported preference activities
- Applications that allow backups
- Debuggable applications
- Application permissions
- Firebase instance(s)
- Sensitive data in code
- Secret API keys
- S3 Bucket storage

## What to look for?
Sensitive data in code, such as usernames, passwords, internal IPs and more...

- **Weak or inappropriate use of cryptography**

can lead to exposure of sensitive data, key leakage, broken authentication, insecure session and spoofing attack.

```sh
grep -r "SecretKeySpec" *
grep -rli "aes" *
grep -rli "iv"
```


- **Exported preference activities**

When an activity is shared with other applications on the device, it is therefore accessible to any other application on the device (exploit this in dynamic analysis).

```sh
cat AndroidManifest.xml | grep activity | grep "android:exported" --color # if true
```


- **Applications that allow backups**

Considered a security issue because people could back up your application via ADB, then get private data from your application on their PC

```sh
cat AndroidManifest.xml | grep "activity:allowBackup" --color # if true
```

- **Debuggable applications**

Enabled on the application, which makes it easier for reverse engineers to attach a debugger to it. This allows dumping a stack trace and accessing debug helper classes. (exploit this in dynamic analysis).

```sh
cat AndroidManifest.xml | grep "activity:debuggable" --color # if true
```

- **Application permissions**

Android will always ask you to approve dangerous permissions.

```sh
cat AndroidManifest.xml | grep "android.permission" --color
```

- **Firebase instance(s)**

Scripts help security analysts identify misconfigured Firebase instances.

```sh
git clone https://github.com/shivsahni/FireBaseScanner
python FireBaseScanner.py -p /path/apk
```

```sh
git clone https://github.com/Sambal0x/firebaseEnum
pip install -r requirements
python firebaseEnum.py -k  /path/apk
```

Example of firebase exploitation:
- https://website.firebaseio.com/.json
- https://website.firebaseio.com/folder/.json


- **Start an exposed activity**
 
```sh
adb shell am start ACTIVITY
# Example: adb shell am start b3nac.injuredandroid/.b25lActivity
```
