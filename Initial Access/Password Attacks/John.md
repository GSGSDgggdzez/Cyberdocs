# John The Ripper

Basic Syntax

```sh
john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

List all formats

```sh
john --list=formats
```

Identify hashes:
- https://hashes.com/en/tools/hash_identifier
- `hashid HASH`
- `hash-identifier HASH`

**Single Crack Mode**
The content of `hash.txt` must be in the following format: `USER:HASH`

```sh
john --single --format=[format] hash.txt
```

## Custom Rules

https://www.openwall.com/john/doc/RULES.shtml
For these attacks, we assume the attacker knows the password policy.

To see all available rules:

```sh
cat /etc/john/john.conf|grep "List.Rules:" | cut -d"." -f3 | cut -d":" -f2 | cut -d"]" -f1 | awk NF
```

Modify the `/etc/john/john.conf` file and add at the end:

```sh
[List.Rules:RULE_NAME]
Az"[0-9][0-9]" ^[!@]
cAz"[0-9] [!£$%@]"
```

We then use regex-style pattern matching to define where the word will be modified

- `Az` Takes the word and appends the characters you define
- `A0` Takes the word and appends the characters you define  
- `c` Capitalizes the character at position

Finally, we must then define which characters should be added, prefixed, or otherwise included. These directly follow the modifier patterns inside double quotes `" "`

- `[0-9]` Will include numbers 0 to 9  
- `[0]` Will only include the digit 0  
- `[A-z]` Will include both uppercase and lowercase  
- `[A-Z]` Will only include uppercase letters  
- `[a-z]` Will only include lowercase letters  
- `[a]` Will only include a  
- `[!£$%@]` Will include the symbols `!£$%@`

Using custom rules

```sh
john --rules=RULE_NAME --wordlist=wordlist.lst hash.txt
#--stdout
```

For more information on rules: https://www.openwall.com/john/doc/RULES.shtml
