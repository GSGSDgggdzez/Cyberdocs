# Cyber Kill Chain®
Designed for the identification and prevention of network intrusions. 

![](Images/cykillchain.png)

## Reconnaissance
This is the planning phase for adversaries, which involves discovering and collecting information about the system and the victim. Using social media sites such as LinkedIn, Facebook, Twitter and Instagram to gather information about a specific target they would like to attack or about the company.

**OSINT** (Open-Source Intelligence) is the first step an attacker must complete to successfully carry out subsequent attack phases by collecting all available information about the company and its employees, such as company size, email addresses and phone numbers, from publicly accessible resources, in order to determine the best target for the attack.

The attacker will have a vast arsenal of tools at their disposal for reconnaissance purposes:

- [theHarvester](https://github.com/laramies/theHarvester) - in addition to collecting emails, this tool is also capable of collecting names, subdomains, IP addresses and URLs using multiple public data sources.
 
- [Hunter.io](https://hunter.io/) - this is an email search tool that will allow you to obtain contact information associated with the domain.

- [OSINT Framework](https://osintframework.com/) - provides the collection of OSINT tools based on various categories.

## Weaponization
After a successful reconnaissance step, attackers would work on creating a "weapon of destruction" such as: `Malware`, `An Exploit`, `A Payload`


- **Malware** is a program or software designed to damage, disrupt or gain unauthorized access to a computer.

- **An Exploit** is a program or code that takes advantage of a vulnerability or flaw in an application or system.

- **A Payload** is malicious code that the attacker executes on the system.

Most attackers typically use automated tools to generate malware or refer to the [DarkWeb](https://www.kaspersky.com/resource-center/threats/deep-web) to purchase malware.

More sophisticated actors or APTs (Advanced Persistent Threat Groups) would write their own custom malware to make the malware sample unique and evade detection on the target.

In the weaponization phase, the attacker:

- Creates an infected Microsoft Office document containing a [malicious macro](https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/) or VBA (Visual Basic for Applications) scripts.

- An attacker can create a malicious payload or a very sophisticated worm, implant it on USB drives, then distribute them publicly.
 
- An attacker would choose Command and Control (C2) techniques to execute commands on the victim's machine or deliver additional payloads.

You can learn more about C2 techniques on [MITRE](https://attack.mitre.org/tactics/TA0011/) [ATT&CK](https://attack.mitre.org/tactics/TA0011/).[](https://attack.mitre.org/tactics/TA0011/)


## Delivery
The delivery phase is where the attacker decides to choose the method of transmitting the malware.

They have many options to choose from:
- Phishing email
- Distributing infected USB drives
- Watering hole attack: designed to target a specific group of people by compromising the website they usually visit, then redirecting them to the malicious website chosen by the attacker.

## Exploitation
After gaining access to the system, the malicious actor could exploit software, system, or server vulnerabilities to elevate their privileges or move laterally across the network.

Here are examples of how an attacker proceeds with exploitation:

- The victim triggers the exploit by opening the email attachment or clicking on a malicious link.
- Using a zero-day exploit.
- Exploiting software, hardware or even human vulnerabilities.
- An attacker triggers the exploit for server-based vulnerabilities.

## Installation
Once the attacker has gained access to the system, they would want to access it again if they lose the connection or if they are detected and the initial access is removed, or if the system is subsequently patched.

This is when the attacker must install a **[persistent backdoor](https://www.offensive-security.com/metasploit-unleashed/persistent-backdoors/)** to allow them to access the system they compromised in the past.

During this phase, the attacker can also use the **[Timestomping](https://attack.mitre.org/techniques/T1070/006/)** technique to avoid being detected by the forensic investigator and also to make the malware appear as part of a legitimate program.

> The `Timestomping` technique allows an attacker to modify file timestamps, including modification, access, creation and change times.


## Command & Control
After persisting and executing malware on the victim's machine, the attacker opens the C2 channel via the malware to remotely control and manipulate the victim.

The compromised endpoint would communicate with an external server configured by an attacker to establish a command and control channel. After establishing the connection, the attacker has full control of the victim's machine.

> Until recently, IRC (Internet Relay Chat) was the traditional C2 channel used by attackers. This is no longer the case, as modern security solutions can easily detect malicious IRC traffic.

The most commonly used C2 channels by adversaries today:

- HTTP/HTTPS protocols: this type of beaconing mixes malicious traffic with legitimate traffic and can help the attacker evade firewalls.
    
- DNS: The infected machine sends constant DNS queries to a DNS server owned by an attacker. This type of C2 communication is also known as **DNS Tunneling.**

> It is important to note that an adversary or another compromised host may own the C2 infrastructure.

## Actions on Objectives (Exfiltration) 

After going through 06 phases, the attacker can finally achieve their objectives, which means acting on the initial objectives.

- Collect user credentials.

- Perform privilege escalation

- Internal reconnaissance

- Lateral movement in the corporate environment.

- Collect and exfiltrate sensitive data.

- Deletion of backups and snapshots.

- Overwriting or corrupting data.
