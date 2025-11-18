# SMB

SMB (Server Message Block) listens by default on ports `139,445`

```sh
nbtscan -r 192.168.45.0/24
```

```sh
nmap -p 139,445 --script=smb-os-discovery <FQDN/IP>
```

Null session authentication on SMB.

```sh
smbclient -L //<FQDN/IP> -N
```

Connect to a specific SMB share.

```sh
smbclient //<FQDN/IP>/<share>
```

Enumerating SMB shares.

```sh
smbmap -H <FQDN/IP>
```

Interaction with the target using RPC.

```sh
rpcclient -U "" <FQDN/IP>
```

Username enumeration using Impacket scripts.

```sh
samrdump.py <FQDN/IP>
```

Enumerating SMB shares using null session authentication.

```sh
crackmapexec smb <FQDN/IP> --shares -u '' -p ''
```

SMB enumeration using enum4linux.

```sh
enum4linux-ng.py <FQDN/IP> -A
```

## Exploitation

**Samba Symlink Directory Traversal.** allow attacker to create a symbolic link to the `root /` partition from writeable share ultimately allowing for read access to the entire file systeme outsite of the share directory.

When a share has write permissions and the `widelinks` parameter set to `yes` is present in the `smb.conf` file

```sh
use auxiliary/admin/smb/samba_symlink_traversal
```

After that access the share with smbclient and we will be able to see a newly created folder

Configuration for Windows pivot

```sh
sudo nano /etc/samba/smb.conf
...
min protocol = SMB2
```

```sh
sudo /etc/init.d/smbd restart
```
