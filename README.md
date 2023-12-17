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
### Docker
```powershell
winget install -e --id Docker.DockerDesktop
```

### Postman
```powershell
winget install -e --id Postman.Postman
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

#### Linux Tools

#### Unzip
```bash
sudo apt-get install unzip
```

Nerd Fonts
```bash
wget -P ~/.fonts 'https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/AnonymousPro.zip'
```
```bash
unzip ~/.fonts/AnonymousPro.zip -d ~/.fonts
```


#### Zsh shell and Oh My Zsh
[Zsh](https://www.zsh.org/), short for Z Shell, is a powerful and feature-rich shell for Unix-like operating systems. It is an extended version of the Bourne Shell (sh) with many improvements and additional features. Zsh is highly customizable and provides an interactive command-line interface, making it popular among advanced users and developers.

```bash
sudo apt install zsh
```
And restart terminal

```zsh
mkdir ~/.fonts
```
```zsh
wget -P ~/.fonts 'https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/AnonymousPro.zip
```

[Oh My Zsh](https://ohmyz.sh/) is an open-source framework and community-driven configuration manager for Zsh. It was created to make it easier for users to manage and customize their Zsh environment. Oh My Zsh provides a collection of themes, plugins, and helper functions that enhance the functionality and appearance of Zsh, making it more user-friendly and visually appealing.
```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Oh My Zsh themes can be fund at [Oh My Zsh on Github | Themes](https://github.com/ohmyzsh/ohmyzsh/tree/master/themes).
1. Open your Zsh configuration file, typically located at ~/.zshrc, in a text editor.
```zsh
vim .zshrc
```
2. Locate the line that sets the ZSH_THEME variable. Assign the desired theme name (without the file extension) to the ZSH_THEME variable.
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```
3. Apply changes
```zsh
source ~/.zshrc
```

*Themes and plugins*

Powerlevel10k

zsh-autosuggestions
Zsh Autosuggestions is a feature that provides intelligent and context-aware suggestions as you type commands in the Zsh shell. It helps you complete your commands more efficiently by offering suggestions based on your command history. This feature is not part of the core Zsh shell but is often added using plugins, and it's a popular choice among Zsh users.

```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Set plugin and apply
```zsh
vim .zshrc
```
```
plugins=(zsh-autosuggestions)
```
```zsh
source ~/.zshrc
```


