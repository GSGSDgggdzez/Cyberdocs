## PowerView
[Cheat Sheet](https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993)

Start PowerView

```sh
. .\PowerView.ps1
```

Enumerate domain users:

```sh
Get-NetUser | select cn
```

Enumerate domain groups:

```sh
Get-NetGroup -GroupName *admin*
```

Display shared folders

```sh
Invoke-ShareFinder
```

Display operating systems running inside the network

```sh
Get-NetComputer -fulldata | select operatingsystem
```
