# Wireshark

## Packet Navigation
Wireshark calculates the number of packets studied and assigns a unique number to each packet.

- **Go to Packet**

Allows you to easily return to a specific point in an event.

```
Go
Go to Packet..
Packet: <NUMBER>
Go to packet
```

- **Find Packets**

Wireshark can search for packets based on their content.

```
Edit
Find Packet...
Packet details | String: <VALUE>
```

**Export Objects (files)**

Wireshark can extract files transferred over the network. Object export is only available for selected protocol streams (DICOM, HTTP, IMF, SMB and TFTP).

```
File
Export Objects
...
```

**Time Display Format**

By default, Wireshark displays time in "seconds since capture start", the common usage is to use the UTC time display format for a better view.

```
View
Time Display Format
UTC Date and Time of Fay (...)
```

## Capturing Kerberose Pre-Auth

If pre-authentication is disabled, anyone can request a TGT on behalf of an account, without sending credentials, and the KDC will return a `KRB_AS_REP` to the requester.

Structure of an `AS-REQ` hash during `Pre-Auth`

```sh
$krb5pa$etype$username$domain$cipher
```

![](./Images/pre-auth-kerberos.png)

```sh
dipeua@probook:~$ hashcat -a 0 -m 19900 hash.txt /opt/rockyou.txt --show

$krb5pa$18$william.dupond$catcorp.local$fc8bbe22b2c967b222ed73dd7616ea71b2ae0c1b0c3688bfff7fecffdebd4054471350cb6e36d3b55ba3420be6c0210b2d978d3f51d1eb4f:.........
```

So pre-authentication for the `william.dupond` account has been disabled
