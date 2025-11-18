# Unconstrained Delegation

How to abuse unconstrained delegation in order to retrieve a user's TGT, thus allowing us to authenticate to any service on their behalf.

# Exploitation

This means that now, with this information, the service can request any service ticket on behalf of the user. I repeat: it can request any. service. ticket. on behalf of the user. It can impersonate the user to authenticate to any service.

Thus, accounts with unconstrained delegation are priority targets for attackers, since once one of these accounts is compromised, they just need to wait for user authentications to be able to authenticate anywhere on their behalf.

# Example

Here is the machine `WEB-SERVER-01` which has "Unconstrained Delegation" on the domain `dom.local`

It is possible to authenticate to this machine to use its network shares. We imagine that an attacker has successfully compromised this machine and is a local administrator on it.

The attacker must then wait for a privileged user to connect to the machine.
They will monitor connections and inspect service tickets to see if a TGT is present in one of them.

For this, they use the `Rubeus` or `kekeo` tool

```
Rubeus monitor /interval:5
```

It turns out that at some point, the support-account, domain administrator, needs to check something on the `WEB-SERVER-01` hard drive. To do this, they connect to the server's network share `\\WEB-SERVER-01\c$`.

This connection is detected by Rubeus.
Since this machine has "Unconstrained Delegation", the service ticket sent by the domain administrator contains a copy of their TGT, which will be extracted by Rubeus.

Now in possession of a domain administrator's TGT (base64 encoded), the attacker can request a service ticket to use the LDAP service of the domain controller `DC-01`.

```
Rubeus.exe asktgs /ticket:<base64 ticket> /service:ldap/dc-01.dom.local /ptt
```

Everything works as expected.
We can verify the presence of the service ticket in memory, for the user (since the attacker used their TGT), and for the LDAP service of the domain controller.

```
klist
```

With this service ticket, it is possible to ask the domain controller to synchronize with the attacker.

Here, the attacker only requested to synchronize the krbtgt account in order to perform a "Golden Ticket" with `mimikatz`

```
lsadump::dcsync /dc:dc-01.dom.local /domain:dom.local /user:krbtgt
```

With the NT hash of the krbtgt account, the attacker can do anything on the Active Directory.
