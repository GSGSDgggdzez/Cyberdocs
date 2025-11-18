# Setting Up

**Linux**

Penetration testing distributions

- [ParrotOS](https://www.parrotsec.org/)
- [Kali](https://www.kali.org/)
- [BlackArch](https://blackarch.org/)
- [Linux BlackBox](https://linux.backbox.org/)

Full update

```sh
sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```

Tools installation

```sh
sudo apt install -y $(cat tools.list | tr "\n" " ")
```

VMware and VirtualBox on Linux

```sh
sudo apt install -y build-essential && sudo bash ~/Downloads/VMware*.bundle
sudo apt install -y virtualbox virtualbox-ext-pack
```

**Windows**

- [CommandoVM](https://github.com/mandiant/commando-vm)
- Manual

```sh
# Updates
PS C:\Temp> Get-ExecutionPolicy -List
PS C:\Temp> Set-ExecutionPolicy Unrestricted -Scope Process #A

# PSWindows Update
PS C:\Temp> Install-Module PSWindowsUpdate
PS C:\Temp> Import-Module PSWindowsUpdate
PS C:\Temp> Install-WindowsUpdate -AcceptAll  
PS C:\Temp> Restart-Computer -Force
```

Package manager [chocolatey](https://docs.chocolatey.org/en-us/choco/commands/install)

```sh
PS C:\Temp> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

Update, verification and installation

```sh
PS C:\Temp> choco upgrade chocolatey -y 
PS C:\Temp> choco install pkg1 pkg2 pkg3 
PS C:\Temp> choco info pkg 
```

Windows Defender exclusions for tools folders.

```sh
PS C:\Temp> Add-MpPreference -ExclusionPath "C:\Users\Dipeua\Tools\"
```

## [Organization](./Organization.md)

## [Virtualization](./Virtualization.md)

## Virtual Private Servers

## [Environment](./Environment.md)

## [AI/LLM](./AI-LLM.md)
