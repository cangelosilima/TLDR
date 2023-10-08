# windows-developer-config

This doc consolidate all installation and configuration needed for a development environment inside a windows 10 machine

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

For WSL installation:
```powersehll
wsl --install
```

After installation, search for linux distribution
```powershell
wsl --list --online
```
Then install it
```powershell
wsl --install -d Ubuntu-20.04
```
