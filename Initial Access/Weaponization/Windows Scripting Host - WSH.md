# Windows Scripting Host - WSH

WSH (Windows Scripting Host) is a built-in Windows administration tool that runs batch files to automate and manage tasks within the operating system.

It is a native Windows engine, `cscript.exe` (for command-line scripts) and `wscript.exe` (for UI scripts), which are responsible for executing various Microsoft Visual Basic (VBScript) scripts, including `vbs` and `vbe`.

Let's now use the VBScript `payload.vbs` to execute executable files.

```js
Set shell = WScript.CreateObject("Wscript.Shell")
shell.Run("C:\Windows\System32\calc.exe " & WScript.ScriptFullName),0,True
```

```sh
wscript c:\Temp\payload.vbs
```


If VBS files are blacklisted, we can then rename the `.vbs` file to `.txt` and execute it as follows:

```sh
wscript /e:VBScript c:\Temp\payload.txt
```
