# Pyramid Of Pain

![](Images/pop.png)

This well-known concept is applied to cybersecurity solutions such as:
- [Cisco Security](https://gblogs.cisco.com/ca/2020/08/26/the-canadian-bacon-cisco-security-and-the-pyramid-of-pain/)
- [SentinelOne](https://www.sentinelone.com/blog/revisiting-the-pyramid-of-pain-leveraging-edr-data-to-improve-cyber-threat-intelligence/)
- [SOCRadar](https://socradar.io/re-examining-the-pyramid-of-pain-to-use-cyber-threat-intelligence-more-effectively/) 

To improve the effectiveness of CTI (Cyber Threat Intelligence), threat hunting and incident response exercises.

## Hash Values (Trivial)


Various online tools can be used to perform hash searches, such as [VirusTotal](https://www.virustotal.com/gui/) and [Metadefender Cloud - OPSWAT](https://metadefender.opswat.com/?lang=en).

## IP Address (Easy)
Knowing the IP addresses used by an adversary allows you to block, drop or deny incoming requests from IP addresses on your perimeter or external firewall.

One way an adversary can make IP blocking difficult is by using Fast Flux.

> Fast Flux is a DNS technique used by botnets to hide phishing, web proxy, malware distribution and malware communication activities behind compromised hosts acting as proxies.
>
> The goal of using Fast Flux network is to make communication between malware and their Command and Control (C&C) server difficult to discover by security professionals.


Thus, the main concept of a Fast Flux network is to have multiple IP addresses associated with a domain name, which is constantly changing.


Read more: [Fast Flux 101: How Cybercriminals Improve the Resilience of Their Infrastructure to Evade Detection and Law Enforcement Takedowns.](https://unit42.paloaltonetworks.com/fast-flux-101/)


## Domain Name (Simple)

Domain names can be a bit more difficult for the attacker to change, as they will likely have to purchase the domain, register it and modify DNS records.

Unfortunately for defenders, many DNS providers offer APIs to allow the attacker to change domains even more easily.

> Punycode is a way to convert words that cannot be written in ASCII to an ASCII Unicode encoding.

attackers use the following URL shortening services to generate malicious links:

- bit.ly
- goo.gl
- ow.ly
- s.id
- smarturl.it
- minuscule.pl
- tinyurl.com
- x.co


## Host Artifacts (Annoying)
Host artifacts are the traces or observables that attackers leave on the system, such as registry values, suspicious process execution, attack patterns or IOCs (Indicators of Compromise), files dropped by malicious applications or anything else unique to the current threat.

## Network Artifacts (Annoying)
A network artifact can be a user agent string, C2 information, or URI patterns followed by HTTP POST requests.

Here are the most common User-Agent strings found for the [Emotet Downloader Trojan.](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/emotet-downloader-trojan-returns-in-force/)

> If you can detect the custom User-Agent strings used by the attacker, you may be able to block them, creating more obstacles and making their attempt to compromise the network more annoying


## Tools (Challeging)
Antivirus signatures, detection rules and YARA rules can be excellent weapons to use against attackers at this stage.

[MalwareBazaar](https://bazaar.abuse.ch/) and [Malshare](https://malshare.com/) are good resources to give you access to samples, malicious feeds and YARA results – all of which can be very helpful when it comes to threat hunting and incident response.

For detection rules, [SOC Prime Threat Detection Marketplace](https://tdm.socprime.com/) is a platform where security professionals share their detection rules for different types of threats, including the latest CVEs being exploited in the wild by adversaries.

**Fuzzy hashing** is also a powerful weapon against the attacker's tools. Fuzzy hashing helps you perform similarity analysis: match two files with minor differences based on fuzzy hash values.

## TTPs (Tough)

If you can detect and respond quickly to TTPs, you leave practically no chance for your adversaries to fight back.

For example, if you could detect a [Pass-the-Hash](https://www.beyondtrust.com/resources/glossary/pass-the-hash-pth-attack) attack using Windows event log monitoring and remediate it, you would be able to find the compromised host very quickly and stop lateral movement inside your network.
