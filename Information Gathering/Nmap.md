# Nmap

## Basic Scan

ICMP network scan (Sweeping)

```sh
nmap -sn 192.168.45.0/24
#nmap -sn 192.168.45.1-254
```

TCP scan (**`connect scan`**) **`SYN | SYN-ACK | ACK`**

```sh
nmap <IP> -sT
```

```sh
nc -v -z -w 1 <FQDN/IP> 80
```

UDP scan (**`stateless`**)

```sh
sudo nmap <IP> -sU --top-ports 20 
sudo nmap <IP> -sU -F -v --top-ports 20
```

```sh
nc -u -v -z -w 1 <IP> 80
```

SYN Scan (**`stealth scan`**) can bypass older IDS **`SYN | SYN-ACK`**

```sh
sudo nmap <IP> -sS
```

## Advanced Scan

Other types of stealth scans used to bypass certain firewalls.

TCP NULL Scan **`<none>`**

```sh
sudo nmap <IP> -sN
```

TCP FIN Scan **`FIN`**

```sh
sudo nmap <IP> -sF
```

TCP Xmas Scan **`FIN, PSH, URG`**

```sh
sudo nmap <IP> -sX
```

TCP Maimon Scan **`FIN, ACK | RST`**
This type of scan is not the first scan you would choose to discover a system and will not work on most targets encountered in modern networks

```sh
sudo nmap <IP> -sM
```

## Identify Firewall rules

`ACK` and `Window` scans expose firewall rules, not services.

TCP ACK Scan **`ACK | RST`**
This type of scan can be useful if there is a firewall in front of the target and is better suited for discovering firewall rule sets and configuration.
The result of this scan shows ports that are not blocked by the firewall

```sh
sudo nmap <IP> -sA
```

Window Scan **`ACK | RST`**
The result of this scan shows ports that are not blocked by the firewall. Ports may display `closed` but they are actually open.

```sh
sudo nmap <IP> -sW
```

Custom scan

```sh
sudo nmap --scanflags {URG,ACK,PSH,RST,SYN,FIN}
```

## Spoofing

Spoofing the source IP address can be an excellent approach for performing a stealth scan. However, it will only work if you can monitor the traffic.

IP Source Spoofing
This scan will be useless if the attacking system cannot monitor the network to obtain responses.

```sh
nmap -e NET_INTERFACE -Pn -S SPOOFED_IP MACHINE_IP
```

MAC Source Spoofing
This address spoofing is only possible if the attacker and target machine are on the same Ethernet network (802.3) or the same Wi-Fi network (802.11).

```sh
nmap -e NET_INTERFACE -Pn --spoof-mac SPOOFED_MAC MACHINE_IP
```

Decoys
Make the scan appear to come from multiple IP addresses so the attacker's IP address is lost among them:

```sh
nmap -D 10.10.0.1,10.10.0.2,RND,RND,ME MACHINE_IP
```

## Firewall evasion 

There are a variety of other useful switches for bypassing firewalls available [here](https://nmap.org/book/man-bypass-firewalls-ids.html) 

- `-f`, `-ff` used to fragment packets (split them into smaller pieces), making it less likely that packets will be detected by a firewall or IDS.

- `--mtu <number>` acts like `-f` but provides more control over packet size. Accepts a maximum transmission unit size to use for sent packets which must be a multiple of 8.

- `--scan-delay <time>ms` used to add a delay between sent packets. This is very useful if the network is unstable, but also to avoid time-based firewall/IDS triggers that might be in place.

- `--badsum` this is used to generate an invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to verify the packet's checksum. As such, this switch can be used to determine the presence of a firewall/IDS.

- `--data-length NUM` increase the size of your packets to make them appear harmless

## Idle scanning

Idle or zombie scanning, requires an idle system connected to the network that you can communicate with

> The Idle scan is a stealth technique that involves the presence of a zombie (host that is not sending or receiving any packets thus) in the target network.


Find a zombie that assigns IP ID both incrementally and globally

```sh
sudo nmap -O -v -n 192.168.x.x/24
```

```
use auxiliary/scanner/ip/ipidseq
```

if **`IP ID Sequence Generation: Incremental`**, this a good zombie

Zombie scan

```sh
sudo nmap -sI ZOMBIE_IP MACHINE_IP
```

```sh
sudo nmap -Pn -sI zombie:port <IP> -v -p 55
```

We are able to scan the target host without sending a single packet from our orinal IP adress

## NSE

The NSE is particularly useful for reconnaissance, given the scope of the script library. Some useful categories include:

- `safe`:- Will not affect the target
- `intrusive`:- Not safe: likely to affect the target  
- `vuln`:- Scan for vulnerabilities
- `exploit`:- Attempt to exploit a vulnerability
- `auth`:- Attempt to bypass authentication for running services 
- `brute`:- Attempt to brute force credentials for running services
- `discovery`:- Attempt to query running services for additional information about the network 

A more exhaustive list can be found [here](https://nmap.org/book/nse-usage.html) 

To run a specific script:

```sh
sudo nmap <FQDN/IP> --script=<script-name>
sudo nmap <FQDN/IP> --script=<script-name>,<script-name>
#sudo nmap 192.168.45.130 --script=vuln
```

Some scripts require arguments

```sh
nmap -p 80 --script <script-name> --script-args <script-name>.<arg-name>='<value>'

#nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'
```

A complete list of scripts and their corresponding arguments (along with use case examples) can be found [here](https://nmap.org/nsedoc/) 

Display help menu for a particular script

```sh
nmap --script-help <script-name>
```
