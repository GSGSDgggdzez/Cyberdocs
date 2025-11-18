# Container

Using containers ensures that computing resources are strictly separated from each other.

## Docker

Any system with Docker Engine installed can use Docker containers.

Docker on Linux

```sh
sudo apt update && sudo apt install -y docker.io
```

Docker on Windows

```sh
C:\> IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
C:\> choco upgrade chocolatey
C:\> choco install docker-desktop
```

**Vagrant**

Vagrant is a tool for creating, configuring, and managing virtual machines or virtual machine environments.

Vagrant on Linux

```sh
sudo apt update -y && sudo apt install virtualbox virtualbox-dkms vagrant
```

Vagrant on Windows

```sh
C:\> IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
C:\> choco upgrade chocolatey
C:\> cinst virtualbox cyg-get vagrant
```
