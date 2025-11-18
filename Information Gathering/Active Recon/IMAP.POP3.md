# IMAP/POP3

## POP3 (Post Office Protocol version 3)

Is a protocol used to download email messages from a server. The mail client connects to the POP3 server, authenticates, downloads new emails before (possibly) deleting them.

POP3 listens on port `110` by default.

Some common POP3 commands are:

- `USER <username>` identifies the user
- `PASS <password>` provides the user's password
- `STAT` requests the number of messages and total size
- `LIST` lists all messages on the server and their sizes
- `RETR <message_number>` retrieves the specified message
- `DELE 1`: marks a message for deletion

```sh
telnet <FQDN/IP> 110

AUTH
+OK
PLAIN
.

USER linda
+OK

PASS Pa$$123
+OK Logged in.

STAT
+OK 4 2216
#+OK nn mm 
# nn = the number of emails in the inbox
# mm = the size of the inbox in bytes

LIST
+OK 4 messages:
1 690
2 589
3 483
4 454
.

RETR 4
+OK 454 octets
Return-path: <user@client.thm>
Envelope-to: linda@server.thm
Delivery-date: Thu, 12 Sep 2024 20:12:42 +0000
Received: from [10.11.81.126] (helo=client.thm)
        by example.thm with smtp (Exim 4.95)
        (envelope-from <user@client.thm>)
        id 1soqAj-0007li-39
        for linda@server.thm;
        Thu, 12 Sep 2024 20:12:42 +0000
From: user@client.thm
To: linda@server.thm
Subject: Your Flag

Hello!
Here's your flag:
THM{TELNET_RETR_EMAIL}
Enjoy your journey!
.


QUIT
+OK Logging out.
```

## IMAP (Internet Message Access Protocol) 

More sophisticated than POP3 and allows you to synchronize your email across multiple devices (and mail clients).

IMAP requires each command to be prefixed with a random string to track the response. So we add `c1`, then `c2`, and so on.
IMAP sends login information in plain text over the network.

IMAP listens on port `143` by default.

Some common IMAP commands are:

- `LOGIN <username> <password>` authenticates the user
- `SELECT <mailbox>` selects the mailbox folder to work with
- `FETCH <mail_number> <data_item_name>` Example fetch 3 body[] to retrieve message number 3, header and body.
- `MOVE <sequence_set> <mailbox>` moves specified messages to another mailbox
- `COPY <sequence_set> <data_item_name>` copies specified messages to another mailbox
- `LOGOUT` logs out


```sh
telnet <FQDN/IP> 143

c1 LOGIN linda Pa$$123
#...
c1 OK LOGIN Ok.

c2 LIST "" "*" # list mail folders
* LIST (\HasNoChildren) "." "INBOX.Trash"
* LIST (\HasNoChildren) "." "INBOX.Drafts"
* LIST (\HasNoChildren) "." "INBOX.Templates"
* LIST (\HasNoChildren) "." "INBOX.Sent"
* LIST (\Unmarked \HasChildren) "." "INBOX"
c2 OK LIST completed

c3 EXAMINE INBOX # check for new messages in the inbox
* FLAGS (\Draft \Answered \Flagged \Deleted \Seen \Recent)
* OK [PERMANENTFLAGS ()] No permanent flags permitted
* 0 EXISTS
* 0 RECENT
* OK [UIDVALIDITY 631694851] Ok
* OK [MYRIGHTS "acdilrsw"] ACL
c3 OK [READ-ONLY] Ok

c4 LOGOUT
```

---

Connect to the POP3s service.

```sh
openssl s_client -connect <FQDN/IP>:pop3s
```

Log in to the IMAPS service using cURL.

```sh
curl -k 'imaps://<FQDN/IP>' --user <user>:<password>
```

Connect to the IMAPS service.

```sh
openssl s_client -connect <FQDN/IP>:imaps
```
