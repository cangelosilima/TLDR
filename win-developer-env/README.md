# Windows Developer Environment
This document compiles all the necessary installation and configuration steps required for setting up a development environment on a Windows 10 machine.

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

Create a .wslconfig file inside your %userprofile% folder to set global settings like memory limit:
```powershell
New-Item -Path $env:USERPROFILE -Name .wslconfig
```
```
[wsl2]
memory=3GB
processors=2
```

> [!NOTE]
> Once WSL and Linux distribution is intalled I used [Linux Or WSL Developer Environment](../linux-developer-env/README.md)

### Azure
[Microsoft Azure](https://azure.microsoft.com/pt-br/) is a cloud computing platform and a suite of services offered by Microsoft. It provides a wide range of cloud services, including computing power, storage, networking, databases, artificial intelligence (AI), machine learning (ML), analytics, Internet of Things (IoT), and mor

Azure CLI. You might need to reboot your computer so installation is complete.
```powershell
winget install -e --id Microsoft.AzureCLI
```

```powershell
az login
```

### Terraform
[Terraform](https://developer.hashicorp.com/terraform) is an open-source infrastructure as code (IaC) tool developed by HashiCorp. It enables users to define and provision infrastructure resources in a declarative configuration language. With Terraform, you can describe the desired state of your infrastructure, and the tool will automatically create, modify, or destroy resources to match that state.

> [!IMPORTANT]
> Please be aware that the  Terraform package within Chocolatey is not directly maintained by HashiCorp. It is recommended to regularly check for newer versions directly on the official Terraform website to ensure that you are using the latest and most secure release. Always refer to the official source for the most up-to-date and reliable information on Terraform packages.

So to install Terraform CLI from chocolatey:
```powershell
choco install terraform
```
