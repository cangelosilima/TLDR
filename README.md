# windows-developer-config

This doc consolidate all installation and configuration needed for a development environment inside a windows 10 machine

> [!IMPORTANT]
> For some installations steps in this tutorial you will need administrator privileges, so for a better experience, open all prompts in Administrator mode

## Developer tools

### Git
```powershell
winget install --id Git.Git -e --source winget
```

### Chocolatey
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

### Visual Studio

#### Code
Download from https://code.visualstudio.com/docs

Code Extensions:
* Themes
  * [Dracula](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)
  * [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
  * [Material Icon](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)
* Compilers
  * [Code Runner](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner)

### Terminal
https://apps.microsoft.com/detail/windows-terminal/9N0DX20HK701?hl=pt-br&gl=BR

### WSL
[Documentation](https://aka.ms/wsl)

For WSL installation, first you need to enable linux subsystem feature and virtual machine
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Once your computer is restarted and WSL 1 is installed, upgrade it to WSL 2 and set it as default
```powersehll
wsl --upgrade
```
```powersehll
wsl --set-default-version 2
```

After WSL 2 upgrade, search for linux distribution and install it
```powershell
wsl --list --online
```
```powershell
wsl --install -d Ubuntu-20.04
```
