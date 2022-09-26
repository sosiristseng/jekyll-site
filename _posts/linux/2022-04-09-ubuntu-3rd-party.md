---
title: "Ubuntu 3rd Party Repositories"
date: 2022-04-09T22:32:52+08:00
tags: ["ubuntu"]
categories: ["Linux"]
---

Adding 3rd party repos for packages not available/outdated in xUbuntu's official repos.

<!--more-->

First of all, install required stuff.

```bash
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl git gnupg-agent software-properties-common
```

## Kubuntu APP and framework updates

Install one of the following two:

`Kubuntu backports`: Latest version of KDE APPs

```bash
sudo add-apt-repository -y ppa:kubuntu-ppa/backports
sudo apt-get update && sudo apt full-upgrade -y
```

`Kubuntu PPA`: bugfix version of KDE APPs

```bash
sudo add-apt-repository -y ppa:kubuntu-ppa/ppa
sudo apt-get update && sudo apt full-upgrade -y
```

## Apt-fast

[apt-fast](https://github.com/ilikenwf/apt-fast) is a wrapper and a drop-in replacement for `apt` that speeds up downloading of packages by parallel downloading packages.

```bash
sudo add-apt-repository -y ppa:apt-fast/stable
sudo apt update
echo debconf apt-fast/maxdownloads string 4 | sudo debconf-set-selections
echo debconf apt-fast/dlflag boolean true | sudo debconf-set-selections
echo debconf apt-fast/aptmanager string apt-get | sudo debconf-set-selections
sudo apt install -y apt-fast
```

## Network

### Brave Browser

Setup [Brave browser](https://brave.com/linux/#linux) repo.

```bash
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list > /dev/null

sudo apt update && sudo apt install -y brave-browser
```

### Vivaldi Browser

```bash
curl -fsSL https://repo.vivaldi.com/archive/linux_signing_key.pub | sudo gpg --dearmor -o /usr/share/keyrings/vivaldi-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/vivaldi-keyring.gpg arch=amd64] https://repo.vivaldi.com/archive/deb/ stable main" | sudo tee /etc/apt/sources.list.d/vivaldi.list > /dev/null

sudo apt update && sudo apt install -y vivaldi-stable
```

### Anydesk

```bash
curl -fsSL https://keys.anydesk.com/repos/DEB-GPG-KEY | sudo gpg --dearmor -o /usr/share/keyrings/anydesk-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/anydesk-keyring.gpg] http://deb.anydesk.com/ all main" | sudo tee /etc/apt/sources.list.d/anydesk-stable.list > /dev/null

sudo apt update && sudo apt install -y anydesk
```

### QBittorrent

```bash
sudo add-apt-repository -y ppa:qbittorrent-team/qbittorrent-stable

sudo apt update && sudo apt install -y qbittorrent
```

### Google drive client

```bash
sudo add-apt-repository -y ppa:alessandro-strada/ppa        # Google drive client

sudo apt update && sudo apt install -y google-drive-ocamlfuse
```

### Onedrive client

[onedrive](https://github.com/abraunegg/onedrive) by `abraunegg`.

```bash
sudo add-apt-repository -y ppa:yann1ck/onedrive
sudo apt update && sudo apt install onedrive -y
```

[onedriver](https://github.com/jstaf/onedriver) by `jstaf` from [OpenSUSE build service](https://software.opensuse.org/download.html?project=home%3Ajstaf&package=onedriver) (OBS).

### Telegram desktop client

[Telegram PPA](https://launchpad.net/~atareao/+archive/ubuntu/telegram)

```bash
sudo add-apt-repository -y ppa:atareao/telegram
sudo apt update && sudo apt install telegram -y
```

## Development tools

### Docker

Please see [supported versions](https://docs.docker.com/engine/install/ubuntu/) before adding the docker repo.

```bash
# Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### Git stable version

```bash
sudo add-apt-repository -y ppa:git-core/ppa

sudo apt update && sudo apt install -y git git-lfs
```

### VSCode

```bash
curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" | sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

sudo apt update && sudo apt install -y code
```

## Document processing

### Libreoffice

Libreoffice lastest version.

```bash
sudo add-apt-repository -y ppa:libreoffice/ppa

sudo apt update && sudo apt install -y libreoffice
```

### Zotero

[Zotero deb](https://github.com/retorquere/zotero-deb) provides packaged versions of Zotero reference manager and Juris-M for Debian-based systems.

```bash
curl -sL https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
sudo apt update && sudo apt install -y zotero
```

## Kernel and drivers

### Mainline kernels for Ubuntu LTS

[New mainline kernels for Ubuntu LTS releases](https://launchpad.net/~tuxinvader/+archive/ubuntu/lts-mainline)

```bash
sudo add-apt-repository -y ppa:tuxinvader/lts-mainline
```

### Xanmod Linux kernel

[Xanmod](https://xanmod.org/) is a general-purpose Linux kernel distribution with custom settings and new features.

```bash
curl -fsSL https://dl.xanmod.org/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/xanmod-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/xanmod-keyring.gpg] http://deb.xanmod.org releases main' | sudo tee /etc/apt/sources.list.d/xanmod-kernel.list > /dev/null

sudo apt update && sudo apt install -y linux-xanmod
```

### Nvidia GPU computing (CUDA)

> The following section is specifically for Ubuntu 20.04 LTS.

Install nvidia CUDA 11 runtime and compatible [GPU driver](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=2004&target_type=debnetwork).

```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
sudo apt-get update && sudo apt-get -y install cuda
```

### AMD and Intel open-source GPU driver (Mesa)

Setup latest Mesa open source GPU drivers.

```bash
sudo add-apt-repository -y ppa:kisak/kisak-mesa
sudo apt update && sudo apt full-upgrade -y
```

## Themes

### Papirus icon themes

[GitHub repos of the Papirus team](https://github.com/PapirusDevelopmentTeam)

```bash
sudo add-apt-repository -y ppa:papirus/papirus

sudo apt update && sudo apt install -y papirus-icon-theme qt5-style-kvantum papirus-folders materia-kde
```
