# MySQL

Login to the MySQL server.

```sh
mysql -u <user> -p<password> -h <FQDN/IP>
```

MySQL enumeration

```sh
nmap --script=mysql-enum <FQDN/IP>
```

```sh
use auxiliary/admin/mysql/mysql_sql
```

Exploit MySQL

Extract password hashes

```sh
use auxiliary/scanner/mysql/mysql_schemadump
```

```sh
use auxiliary/scanner/mysql/mysql_hashdump
```
