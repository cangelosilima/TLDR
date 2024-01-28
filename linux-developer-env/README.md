# Linux Or WSL Developer Environment
This document compiles all the necessary installation and configuration steps required for setting up a development environment on am Ubuntu 20.04.6 LTS machine.

> [!IMPORTANT]
> For some installations steps in this tutorial you will need administrator privileges, so for a better experience, execute with `sudo`

## apt-get
The apt-get command is a package management tool used in Debian-based Linux distributions, such as Ubuntu. It allows users to install, upgrade, or remove software packages on their systems.

## List and upgrade installed packages
```bash
sudo apt-get update 
```
```bash
sudo apt-get upgrade
```

## Unzip
```bash
sudo apt-get install unzip
```

## Zsh shell and Oh My Zsh
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


## NFS
NFS, stands for "Network File System". NFS is a distributed file system protocol that allows a user on a client computer to access files over a network as if they were on the local computer. It enables remote access to files and directories.

For some projects in using Kubernetes persistence volumes I used a NFS Server to store data, so I used [nfs-server-alpine](https://hub.docker.com/r/itsthenetwork/nfs-server-alpine) and centralized at /data/nfs-storage
```zsh
sudo mkdir -p /data/nfs-storage
```
```zsh
sudo mkdir -p /mnt/nfs
```
```zsh
sudo chown 1000:1000 nfs
```
```zsh
sudo mount.nfs4 -v 10.10.10.69:/ /data/nfs-storage
```

Install NFS Cliente
```zsh
sudo apt install nfs-common -y
```

## Azure

If you install on windows envorionment it will reflect on wsl

So modify the profile file ~/.profile by adding the following:
```
export KUBECONFIG=/mnt/c/Users/<windows user>/.kube/config
```


