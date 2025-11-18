# IPTable

Configure a firewall to respond with an `RST` packet

```sh
sudo iptables -I INPUT -p tcp --dport <port> -j REJECT --reject-with tcp-reset
```
