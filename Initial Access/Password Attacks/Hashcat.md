# Hashcat

- `?d` tells hashcat to use a digit

## Dictionary

A dictionary attack is a technique used to guess passwords using well-known words or phrases.

```sh
hashcat -a 0 -m <mode> hash.txt wordlist.lst
```

## Brute Force 

Brute forcing is a common attack used by attackers to gain unauthorized access to a personal account. 

```sh
hashcat -a 3 -m <mode> hash.txt wordlist.lst
```

```sh
hashcat -a 3 -m 0 05A5CF06982BA7892ED2A6D38FE832D6 ?d?d?d?d
```
