# Shell

We can force the remote server either to send us command line access ([Reverse shell](./Reverse%20shell.md)), or to open a port on the server to which we can connect in order to execute other commands ([Bind shell](./Bind%20shell.md)).


## TTY
Shell stabilization

BASH

```sh
/usr/bin/script -qc /bin/bash /dev/null
export TERM=xterm
```

Python

```sh
python -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm
clear
Ctrl + Z
stty raw -echo; fg
```
