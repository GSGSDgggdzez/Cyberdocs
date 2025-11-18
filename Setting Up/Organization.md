# Organization

When organizing our activities or those of an entire team, we must ensure that we follow a specific procedure. Everyone must know where they stand and where each member intervenes throughout the penetration testing process. It is also essential to have a common understanding of each member's activities. Otherwise, elements may end up in the wrong subdirectory, or evidence necessary for creating reports could be lost or corrupted.

## Password Manager

- [1Password](https://1password.com/)
- [LastPass](https://www.lastpass.com/)
- [Keeper](https://www.keepersecurity.com/)
- [Bitwarden](https://bitwarden.com/)
- [Proton Pass](https://proton.me/pass)

## Note Taking

- [Notion.so](https://notion.so/)
- Anytype
- [Obsidian](https://obsidian.md/)
- [Xmind](https://xmind.com/) mind map editor that can visualize relevant information components and processes very well

For Pentest Report Generator

- [GhostWriter](https://github.com/GhostManager/Ghostwriter) and [Pwndoc](https://github.com/pwndoc/pwndoc) allow us to generate our documentation and have a clear overview of the steps taken.

**Logging**

Logging is essential both for documentation and for our protection. If third parties attack the company during our penetration test and damage occurs, we can prove that this damage did not result from our activities. For this, we can use the `script` and `date` tools.

Date to display the exact date and time of each command in our command line. With script, every command and its result is saved to a background file. To display the date and time, we can replace the `PS1` variable in our `.bashrc` file with the following content.

```sh
PS1="\[\033[1;32m\]\342\224\200\$([[ \$(/opt/vpnbash.sh) == *\"10.\"* ]] && echo \"[\[\033[1;34m\]\$(/opt/vpnserver.sh)\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\$(/opt/vpnbash.sh)\[\033[1;32m\]]\342\224\200\")[\[\033[1;37m\]\u\[\033[01;32m\]@\[\033[01;34m\]\h\[\033[1;32m\]]\342\224\200[\[\033[1;37m\]\w\[\033[1;32m\]]\n\[\033[1;32m\]\342\224\224\342\224\200\342\224\200\342\225\274 [\[\e[01;33m\]$(date +%D-%r)\[\e[01;32m\]]\\$ \[\e[0m\]"
```

To start logging with script (on Linux) and Start-Transcript (on Windows), we can use the following command

```sh
$ script 03-21-2021-0200pm-exploitation.log
$ <ALL THE COMMANDS>
$ exit
```

```sh
C:\> Start-Transcript -Path "C:\Pentesting\03-21-2021-0200pm-exploitation.log"

Transcript started, output file is C:\Pentesting\03-21-2021-0200pm-exploitation.log

C:\> ...SNIP...
C:\> Stop-Transcript
```

- We can use an application called [Peek](https://github.com/phw/peek) to create GIFs that record all necessary actions.
