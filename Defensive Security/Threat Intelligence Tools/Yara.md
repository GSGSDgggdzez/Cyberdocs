# Yara

Yara can identify information based on `binary patterns` and `textual patterns` in a file.

> For example, Yara rules are frequently written to determine whether a file is malicious or not, based on the features (or patterns) it presents.

## Yara Rules

> Your rule is only effective if you understand the patterns you want to search for.
> 
> Each rule must have a name and a condition.

**Anatomy of a Yara Rule**

![](../Fundamentals/Cyber%20Defence%20Frameworks/Images/yara.png)

Create a file named: `myrules.yar`:

```sh
rule examplerule {
    meta:
        author = "Dipeua"
        description = "Demo"
    
    strings:
        pseudo = "Ber1y"
        skill = "Jr Analyste"

    condition: true
    
}
```

Execute a yara rule

```sh
yara myrules.yar somedirectory
yara myrules.yar somefile
```

- [Conditions](https://yara.readthedocs.io/en/stable/writingrules.html)
- [Cheat sheet](https://medium.com/malware-buddy/security-infographics-9c4d3bd891ef#18dd)

## Yara Modules

The following frameworks can improve the technicality of Yara rules:

- [Cuckoo Sandbox](https://cuckoosandbox.org/): Automated malware analysis environment. Allows generating Yara rules based on behaviors discovered from Cuckoo Sandbox.

- [Python PE](https://pypi.org/project/pefile/): Allows creating Yara rules from different sections and elements of the Windows Portable Executable (PE) structure.

## Yara Tools

- [Loki](https://github.com/Neo23x0/Loki/blob/master/README.md) is an IOC scanner

```sh
python loki.py --update
python loki.py -p .
```

- [THOR Lite](https://www.nextron-systems.com/thor-lite/) is also an IOC scanner but uses fewer CPU resources

- [Fenrir](https://github.com/Neo23x0/Fenrir)

- [YaYa](https://www.eff.org/deeplinks/2020/09/introducing-yaya-new-threat-hunting-tool-eff-threat-lab) Manages multiple YARA rule repositories, then allows researchers to add their own rules, disable others.

- [yarGen](https://github.com/Neo23x0/yarGen) is a YARA rule generator

> The principle is creating Yara rules from strings found in malware files.

Generate a Yara rule for file2

```sh
python3 yarGen.p --update
python3 yarGen.py -m /home/cmnatic/suspicious-files/file2 --excludegood -o /home/cmnatic/suspicious-files/file2.yar
```

- [yarAnalyzer](https://github.com/Neo23x0/yarAnalyzer/)

- [Valhalla](https://www.nextron-systems.com/valhalla/) is an online Yara feed

# Resources

Further reading on creating Yara rules and using yarGen

- [https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/](https://www.bsk-consulting.de/2015/02/16/write-simple-sound-yara-rules/)      
- [https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/](https://www.bsk-consulting.de/2015/10/17/how-to-write-simple-but-sound-yara-rules-part-2/)
- [https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/](https://www.bsk-consulting.de/2016/04/15/how-to-write-simple-but-sound-yara-rules-part-3/)
