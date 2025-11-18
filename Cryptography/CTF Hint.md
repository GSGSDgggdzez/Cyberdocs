# CTF Hint

The key variables you need to know for RSA in CTFs are: `p, q, m, n, e, d, c`

- `p and q` are large prime numbers, `n` is the product of `p and q`.

```sh
n = (p * q)
```

- The public key is `n and e`, the private key is `n and d`.

```sh
public_key = n & e
private_key = n & d
```

- `m` is used to represent the message (in plaintext) and `c` represents the ciphertext (encrypted text).

```sh
clear_text = m
cipher_text = c
```
