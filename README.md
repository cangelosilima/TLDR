# windows-developer-config

This doc consolidate all installation and configuration needed for a development environment inside a windows 10 machine

## Developer tools

Git
```powershell
winget install --id Git.Git -e --source winget
```

Chocolatey
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```
