## WHOIS

WHOIS lookup for the target.

```sh
whois target.com
```

Reverse Lookup Brute Force

```sh
for ip in $(seq 50 100); do host X.X.X.$ip; done | grep -v "not found"
```

## DNS Enumeration

Identify records for the target

```sh
nslookup -query=[A, AAAA, PTR, MX, TXT, ANY, NS] target.com

dig [A, AAAA, PTR, MX, TXT, ANY] target.com @<nameserver/IP>
dig -x <IP> @<nameserver/IP>
```

```sh
# AXFR request to the specific nameserver. 
dig axfr target.com @<nameserver>
dig axfr target.com @NSZTM1.DIGI.NINJA | cut -d " " -f3
```

## Passive Subdomain Enumeration

- [VirusTotal](https://www.virustotal.com/gui/home/search)
- Project Sonar

```sh 
# All subdomains for a given domain.
curl -s https://sonar.omnisint.io/subdomains/target.com | jq -r '.[]' | sort -u 

# All TLDs found for a given domain.
curl -s https://sonar.omnisint.io/tlds/target.com | jq -r '.[]' | sort -u      

# All results across all TLDs for a given domain.
curl -s https://sonar.omnisint.io/all/target.com | jq -r '.[]' | sort -u       

# Reverse DNS lookup on IP address
curl -s https://sonar.omnisint.io/reverse/{ip}        

# Reverse DNS lookup of a CIDR range
curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} 
```

**Certificate Transparency.**

SSL/TLS certificates are another interesting source of information for extracting subdomains.

- https://search.censys.io/
- https://crt.sh

```sh
# Certificate transparency.
curl -s "https://crt.sh/?q=target.com&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "crt.sh_ouput.txt"
```

```sh
openssl s_client -ign_eof 2>/dev/null <<<$'HEAD / HTTP/1.0\r\n\r' -connect "target.com" | openssl x509 -noout -text -in - | grep 'DNS' | sed -e 's|DNS:|\n|g' -e 's|^\*.*||g' | tr -d ',' | sort -u
```

**theHarvester**

```sh
export TARGET=target.com

# Collect information from these sources.
cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done

# Extract all found subdomains and sort them
cat *.json | jq -r '.hosts[]' 2>/dev/null | cut -d':' -f 1 | sort -u > "${TARGET}_theHarvester.txt"

# Merge all files
cat $TARGET_*.txt | sort -u > $TARGET_subdomains_passive.txt
```

Reverse IP lookup to find other servers sharing the same IP addresses:

- [View DNS](https://viewdns.info)
- [Threati Intelligence Platform](https://threatintelligenceplatform.com/)
## Passive Infrastructure Identification

- [Netcraft](https://sitereport.netcraft.com)
- [WayBackMachine](http://web.archive.org/)

Inspect URLs recorded by [Wayback Machine]([https://github.com/tomnomnom/waybackurls](https://github.com/tomnomnom/waybackurls)) and search for specific keywords

```sh
waybackurls -dates https://target.com > waybackurls_output.txt
```

## Active Subdomain Enumeration

- [Zone Transfers](https://hackertarget.com/zone-transfer/)
- [HackerTarget]([https://hackertarget.com/zone-transfer/](https://hackertarget.com/zone-transfer/))

```sh
# Identify name servers
nslookup -type=NS target.com

# Zone transfer using Nslookup on the target domain and its name server.
nslookup -type=any -query=AXFR target.com <nameserver>
```

> If we manage to perform a successful zone transfer for a domain, there is no need to continue enumerating that particular domain as it will extract all available information.

## Active Infrastructure Identification

```sh
# Technology identification.
whatweb -a 3 https://target.com -v

# WAF fingerprinting.
wafw00f -v https://target.com
```

[Aquatone]([https://github.com/michenriksen/aquatone](https://github.com/michenriksen/aquatone)) to perform screenshots for a list of subdomains

```sh
cat subdomains_output.txt | aquatone -out ./aquatone -screenshot-timeout 1000
```
