# SNMP

SNMP (Simple Network Management Protocol) is a network management protocol that allows monitoring and managing network equipment, such as routers, switches, servers, etc.

It allows collecting information on network status and performance, remotely configuring equipment, detecting and resolving problems proactively.

The default manufacturer **community strings** are `manager`, `public` and `private`.

In SNMP versions 1 and 2c, access is controlled using a plaintext community string, and if we know the name, we can access it.

The SMTP server listens on port 161 by default.

Enumerate which `community` is enabled on the server

```sh
nmap -sU -p 161 --script=snmp-brute <IP>
```


Bruteforcing community strings of the SNMP service.

```sh
onesixtyone -c dict.txt <FQDN/IP>
```

Querying OIDs using snmpwalk.

```sh
snmpwalk -v 2c -c <community string> <FQDN/IP>
```

Bruteforcing SNMP service OIDs.

```c
braa <community string>@<FQDN/IP>:.1.*
braa <community string>@<FQDN/IP>:.1.3.6.*
```

Display installed or available programs on the machine

```sh
snmpwalk -v 2c -c <community string> <FQDN/IP> hrSWInstalledName
```

Enumerating the entire MIB Tree

```sh
snmpwalk -c public -v1 -t 10 <FQDN/IP> 
```

Enumerating Windows users

```sh
snmpwalk -c public -v1 <FQDN/IP> 1.3.6.1.4.1.77.1.2.25
```

Enumerating running windows processes

```sh
snmpwalk -c public -v1 <FQDN/IP> 1.3.6.1.2.1.25.4.2.1.2
```

Enumerating open TCP ports

```sh
snmpwalk -c public -v1 <FQDN/IP> 1.3.6.1.2.1.6.13.1.3
```

Enumerating installed software

```sh
snmpwalk -c public -v1 <FQDN/IP> 1.3.6.1.2.1.25.3.1.2
```

Search for this

```sh
snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0
```
