# PortMapper

Runs on TCP/UDP port 111 and 32771 used with [NFS](./NFS.md)
Used to map all `Open Network Computing Remote Prodecure Call`

Allows to see which ports are open locally on the system (localhost)

```sh
nmap -sV -p 111 --script=rpc-grind,rpcinfo <FQDN/IP>
```


```
rpcinfo -p <FQDN/IP>
```

Interaction with the target using RPC.

```sh
rpcclient -U "" <FQDN/IP>
```

**RID Cycling**

Manually query each individual user RID

```sh
for i in $(seq 500 2000); do echo "queryuser $i" |rpcclient -U "" -N 10.211.11.10 2>/dev/null | grep -i "User Name"; done
```
