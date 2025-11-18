# LDAP (Lightweight Directory Access Protocol)

In LDAP authentication, the application directly verifies the user's credentials.

The application has a pair of AD credentials that it can use first to query LDAP, then verify the AD user's credentials.

## Anonymous Bind

Query the LDAP server root to get its basic information by performing an anonymous bind.

```sh
ldapsearch -x -H ldap://10.211.11.10 -s base
```

Search for all objects of type "person" in the LDAP domain `dc=home,dc=local` and list users defined in the `home.local` domain

```sh
ldapsearch -x -H ldap://10.211.11.10 -b "dc=home,dc=local" "(objectClass=person)"
```

## Pass-back Attack

Attack conducted against LDAP authentication mechanisms after obtaining initial access to the internal network.

Can be performed when we access the configuration of a device where LDAP settings are specified.

## LDAP + PowerView

Create a session on the compromised machine to execute remotely

```sh
$session = New-PSSession -ComputerName 192.168.1.1 -Credential username
Enter-PSSesion $session
```

Get the list of domain controllers on the network:

```sh
nltest /dclist:pwnlab.local
```
