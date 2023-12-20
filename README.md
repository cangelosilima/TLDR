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
[Chocolatey](https://chocolatey.org/) is a package manager for Windows that automates the process of software installation, configuration, and maintenance. It provides a command-line interface (CLI) and a centralized repository of software packages, allowing users to easily install, update, and manage software on Windows systems.

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1')) 
```
```powershell
SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

### Docker
```powershell
winget install -e --id Docker.DockerDesktop
```

### Postman
```powershell
winget install -e --id Postman.Postman
```

### k6
[k6](https://k6.io/) is an open-source performance testing tool that is used for testing the performance of APIs, microservices, and websites. It allows developers and QA engineers to create and run performance tests to evaluate the scalability and reliability of their applications.
```powershell
choco install k6
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

#### Nerd Fonts
Nerd Fonts is a collection of over-the-top, monospaced fonts designed for programming and development. These fonts not only include the standard Latin alphabet characters but also a wide range of symbols, icons, and glyphs commonly used in programming, terminal applications, and text editors. The term "Nerd Fonts" is often associated with fonts that have extensive coverage of programming-related symbols.

```powershell
choco install nerd-fonts-meslo
```

*Change Windows Terminal settings to use Nerd-Fonts*
Because we want Windows Terminal to be able to render the icons in the powerlevel10k theme correctly, we need to change the Windows Terminal configuration to use the Nerd-Font we've downloaded before. Click on Settings in the Windows Terminal menu and edit the settings.json file with your favorite text editor.

Find your wsl2 profile and add the line 
```json
"fontFace": "MesloLGL Nerd Font"
```

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

#### Zsh shell and Oh My Zsh
[Zsh](https://www.zsh.org/), short for Z Shell, is a powerful and feature-rich shell for Unix-like operating systems. It is an extended version of the Bourne Shell (sh) with many improvements and additional features. Zsh is highly customizable and provides an interactive command-line interface, making it popular among advanced users and developers. Oh My Zsh themes can be fund at [Oh My Zsh on Github | Themes](https://github.com/ohmyzsh/ohmyzsh/tree/master/themes).

```bash
sudo apt install zsh
```
[Oh My Zsh](https://ohmyz.sh/) is an open-source framework and community-driven configuration manager for Zsh. It was created to make it easier for users to manage and customize their Zsh environment. Oh My Zsh provides a collection of themes, plugins, and helper functions that enhance the functionality and appearance of Zsh, making it more user-friendly and visually appealing.
```zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Oh My Zsh themes can be fund at [Oh My Zsh on Github | Themes](https://github.com/ohmyzsh/ohmyzsh/tree/master/themes).


*Themes and plugins*

[Powerlevel10k](https://github.com/romkatv/powerlevel10k ) is a highly customizable Zsh theme designed for users who want a feature-rich and visually appealing command-line prompt. It is built on top of the Powerlevel9k theme and provides additional features and performance improvements. Powerlevel10k is known for its flexibility, extensive configuration options, and fast rendering speed.

```zsh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
```
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

[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) is a feature that provides intelligent and context-aware suggestions as you type commands in the Zsh shell. It helps you complete your commands more efficiently by offering suggestions based on your command history. This feature is not part of the core Zsh shell but is often added using plugins, and it's a popular choice among Zsh users.

```zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
1. Open your Zsh configuration file, typically located at ~/.zshrc, in a text editor.
```zsh
vim .zshrc
```
2. Locate the line that sets the plugins variable. Append the desired plugin name (without the file extension) to the plugins E variable.
```
plugins=(git zsh-autosuggestions)
```
3. Apply changes
```zsh
source ~/.zshrc
```

[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) is a Zsh plugin that provides syntax highlighting for commands as you type them in the terminal. This makes it easier to visually identify and correct any mistakes in your commands before executing them. The syntax highlighting is based on the syntax rules of the Zsh shell.

```zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
1. Open your Zsh configuration file, typically located at ~/.zshrc, in a text editor.
```zsh
vim .zshrc
```
2. Locate the line that sets the plugins variable. Append the desired plugin name (without the file extension) to the plugins E variable.
```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```
3. Apply changes
```zsh
source ~/.zshrc
```
