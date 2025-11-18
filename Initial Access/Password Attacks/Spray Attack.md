# Spray Attack

A password spray attack targets many usernames using a common weak password, which could help avoid an account lockout policy.

To succeed with a password spray attack, we must enumerate the target and create a list of valid usernames (or a list of email addresses).

RPD 
[RDPassSpray](https://github.com/xFreed0m/RDPassSpray)  

```sh
python3 RDPassSpray.py
```

Outlook Web Access (OWA)

- [SprayingToolkit](https://github.com/byt3bl33d3r/SprayingToolkit) (atomizer.py)
- [MailSniper](https://github.com/dafthack/MailSniper)

```sh
msf6> search owa_login
```

SMB

```sh
use auxiliary/scanner/smb/smb_login
```

SMTP

```sh
use auxiliary/scanner/smtp/smtp_enum
```
