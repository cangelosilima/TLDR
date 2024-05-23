# Windows Developer Environment
This document compiles all the necessary installation and configuration steps required for setting up a development environment on a Windows 10 machine.

<p align="right">(<a href="../README.md">back to beginning</a>)</p>

> [!IMPORTANT]
> For some installations steps in this tutorial you will need administrator privileges, so for a better experience, open all prompts in Administrator mode


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#developer-tools">Developer Tools</a>
      <ul>
        <li><a href="#git">Git</a></li>
        <li><a href="#chocolatey">Chocolatey</a></li>
        <li><a href="#docker">Docker</a></li>
        <li><a href="#postman">Postman</a></li>
        <li><a href="#k6">k6</a></li>
        <li><a href="#visual-studio">Visual Studio</a></li>
        <li><a href="#terminal">Terminal</a></li>
        <li><a href="#wsl">WSL</a></li>
      </ul>
    </li>
    <li>
      <a href="#cloud-and-iac">Cloud and IaC</a>
      <ul>
        <li><a href="#azure">Azure</a></li>
        <li><a href="#terraform">Terraform</a></li>
      </ul>
    </li>
  </ol>
</details>

## Developer Tools

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

Find your wsl2wsl add the line 
```json
"fontFace": "MesloLGL Nerd Font"
```

### WSL
[DocumentationWSL://aka.ms/wsl)wsl wsl installationWSL you need to enable linux subsystem feature and virtual machine
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Once your computer is restarted and wsl 1WSL, upgrade it to wsl 2WSL it as default
```powersehll
wsl --wsl
```powersehll
wsl --wsl-version 2
```

After wsl 2WSL search for linux distribution and install it
```powershell
wsl --wslonline
```
```powershell
wsl --wsl Ubuntu-20.04
```

Create a .wslconfigwsl your %userprofile% folder to set global settings like memory limit:
```powershell
New-Item -Path $env:USERPROFILE -Name .wslconfigwsl
[wsl2wsl=3GB
processors=2
```

> [!NOTE]
> Once wsl andWSL is intalled I used [Linux Or wsl DeveloperWSLlinux-developer-env/README.md)

<p align="right">(<a href="#windows-developer-environment">back to top</a>)</p>

## Cloud and IaC

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
<p align="right">(<a href="#windows-developer-environment">back to top</a>)</p>


### Python
[Python](https://www.python.org/) is a high-level, interpreted programming language known for its simplicity and readability, making it a popular choice for beginners and experienced developers alike. Created by Guido van Rossum and first released in 1991, Python emphasizes code readability and simplicity, using significant indentation to define code blocks rather than curly braces or keywords.

To install Python from chocolatey. After that restart your computer.
```powershell
choco install python --version=3.12.3 -y
```

Chocolatey installation should add Python installation path to `PATH` environment variable. But if that doesn't happen you shoukd add it manually:
```powershell
[System.Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Python312;C:\Python312\Scripts", [System.EnvironmentVariableTarget]::Machine)
```

To check if Python is corretly installed, run:
```
python --version
```

If you receive the following error, there will be an aditional step to disable one of the two paths of python installed:
```
Python was not found; run without arguments to install from the Microsoft Store, or disable this shortcut from Settings > Manage App Execution Aliases.
```
```powershell
Remove-Item -Path "C:\Users\cange\AppData\Local\Microsoft\WindowsApps\python.exe"
```

`pip` is the package installer for Python, which allows you to install and manage additional libraries and dependencies that are not included in the standard Python library. To install it:
```

