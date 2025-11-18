# TCPDump

## Basic Capture Options
These options can be chained to define how the tool's output is displayed to us in STDOUT

|          Options          | Result                                                                                                                      |
| :---------------------------: | --------------------------------------------------------------------------------------------------------------------------------- |
|              `-D`               | Displays all available interfaces for capture.                                                                        |
|              `-i`               | Selects an interface from which to perform capture. ex. `-i eth0`                                                |
|              `-n`               | Do not resolve host names.                                                                                                 |
|              `-nn`              | Do not resolve host names or well-known ports.                                                                             |
|              `-e`               | Will retrieve the Ethernet header as well as upper layer data.                                                         |
|              `-X`               | Display packet contents in hexadecimal and ASCII.                                                                       |
|              `-XX`              | Same as X, but will also specify Ethernet headers. (like using `Xe`)                                         |
|         `-v, -vv, -vvv`         | Increase verbosity of displayed and recorded outputs.                                                                     |
|              `-c`               | Capture a specific number of packets, then exit the program.                                                                |
|              `-s`               | Sets the amount of a packet to capture.                                                                                      |
|              `-S`               | Change relative sequence numbers in capture display to absolute sequence numbers. (13248765839 instead of 101) |
|              `-q`               | Print less protocol information.                                                                                       |
|        `-r file.pcap`        | Read from a file.                                                                                                       |
|        `-w file.pcap`        | Write to a file                                                                                                            |
| `-t , -tt, -ttt, -tttt, -ttttt` | To handle 0 timestamps 1                                                                                                    |
---

Capture on an interface

```sh
sudo tcpdump -i (interface) -<options>
sudo tcpdump -i eth0 -nnvXX
```

Listen on a port

```sh
sudo tcpdump port 9001 -A
```

Filter a Wireshark `.pcap` file

```sh
sudo tcpdump -n -r file.pcap
sudo tcpdump -n src host <IP> -r read.pcap
sudo tcpdump -n dst host <IP> -r read.pcap
sudo tcpdump -n port <PORT> -r read.pcap
```

## Packet Filtering

| Filter         | Result                                                                                                                               |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `host`               | `host` will filter visible traffic to show everything involving the designated host. Bidirectional                                         |
| `src / dst`          | `src` and `dest` are modifiers. We can use them to designate a source or destination host or port.                 |
| `net`              | `net` will show us all traffic from or to the designated network. It uses the / notation.                                           |
| `proto`              | will filter for a specific protocol type. (Ether, TCP, UDP and ICMP for examples)                                                      |
| `port`               | `port` is bidirectional. It will display all traffic with the specified port as source or destination.                                      |
| `portrange`          | `portrange` allows us to specify a range of ports. (0-1024)                                                                           |
| `less / greate "<>"` | `less` and `greater` can be used to look for a packet or protocol option of a specific size.                          |
| `and / &&`           | `and` `&&` can be used to concatenate two different filters together. for example, src host AND port.                          |
| `or`                 | `or` allows a match on either of the two conditions. It is not necessary for both to be fulfilled. This can be tricky. |
| `not`                | `not` is a modifier that says everything except x. For example, not UDP.                                                                        |
```sh
sudo tcpdump <filtering> [<options>]
```

```sh
sudo tcpdump -i (interface) host (ip)
sudo tcpdump -i (interface) port (#)
sudo tcpdump -i (interface) proto (#)
sudo tcpdump -i (interface) (protoname)
```

## TCP Flag Specification

1. To match all packets with _`a single TCP flag`_ specified:

```
tcp[tcpflags] == tcp-ack/tcp-syn/tcp-fin/tcp-push/tcp-urg/tcp-rst
```

For example, this displays packets with only the `PSH` flag set.

```
tcp[tcpflags] == tcp-push
```

2. To match packets with _`multiple TCP flags`_ specified:

- You must convert the flags to a decimal value and use that number in

```
tcp[tcpflags] == x
```

![](./Images/indicator.png)

For example, for packets with `PSH` and `ACK` flags set, the decimal value becomes `00011000 = 24`, and the expression becomes

```
tcp [tcpflags] == 24
```

![](./Images/indicator-cmd.png)



