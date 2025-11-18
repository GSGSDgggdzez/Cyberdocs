# SMTP

SMTP (Simple Mail Transfer Protocol) is used to communicate with a mail server for sending emails. It listens on port `25` by default.

SMTP uses plain text, where all commands are sent without encryption

We will use `telnet` to connect to an SMTP server and act as a mail client

Once connected, we issue:
- `helo hostname` then begin typing our email.
- After `helo`, we issue `mail from:`, `rcpt to:` to indicate the sender and recipient.
- When we send our email, we issue the `data` command and type our message. 
- We issue `<CR><LF>.<CR><LF>` (or `Enter . Enter`). 

The SMTP server now queues the message.


```sh
telnet <FQDN/IP> 25
Trying MACHINE_IP...
Connected to MACHINE_IP.
Escape character is '^]'.
220 bento.localdomain ESMTP Postfix (Ubuntu)

HELO telnet
250 bento.localdomain

MAIL FROM: <send@gmail.com>
250 2.1.0 Ok

RCPT TO: <recipient@gmail.com>
250 2.1.5 Ok

DATA
354 End data with .

From: send@gmail.com
To: recipient@gmail.com
SUBJECT: Sending email with Telnet

Hello Frank,
I am just writing to say hi!             
.

250 2.0.0 Ok: queued as C3E7F45F06
QUIT

221 2.0.0 Bye
Connection closed by foreign host.
```

Enumerate which options `verbs` are enabled on the mail server

```sh
nmap --script=smtp-commands -p 25 <IP>
```

Enumerate users manually

```sh
RCPT TO: <user@domain.com>
EXPN <username>
VRFY <username.
```

User enumeration

```sh
smtp-user-enum -M VRFY -U usernames.txt -t 192.168.45.130
```

```sh
use auxiliary/scanner/smtp/smtp_enum
```
