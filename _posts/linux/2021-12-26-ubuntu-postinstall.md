---
title: "Ubuntu Postinstall"
date: 2021-12-26T14:53:29+08:00
tags: ["postinstall", "ubuntu"]
categories: ["Linux"]
---

Things to do after installing

- [Ubuntu](https://ubuntu.com/download)
- [Kubuntu](https://kubuntu.org/)
- [KDE Neon](https://neon.kde.org/), which is based on Ubuntu LTS.
- [WSL2](https://docs.microsoft.com/zh-tw/windows/wsl/install)

<!--more-->

## Traditional Chinese Locale

Default locale in Ubuntu for traditional Chinese (Taiwan) is `lzh_TW` rather than `zh_TW`.

Setup the locale by editing the file

```bash
sudo nano /etc/locale.gen
```

comment the `lzh_TW` line and uncomment the `zh_TW` line. And then run:

```bash
sudo locale-gen
```

Install the Traditional Chinese locale in `Language Support` and then set locale to `Taiwan` to solve this problem.

## Make software repo point to NCHC for faster network speed

If `apt` uses `archive.ubuntu.com` in `/etc/apt/sources.list`, change lines of `archive.ubuntu.com` to `tw.archive.ubuntu.com` or `free.nchc.org.tw`.

```bash
sudo sed -i 's/us.archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list
sudo sed -i 's/archive.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list
sudo sed -i 's/security.ubuntu.com/free.nchc.org.tw/g' /etc/apt/sources.list
sudo apt clean && sudo apt update && sudo apt full-upgrade -y
```

## Setup 3rd party repos

See [Setup Ubuntu 3rd party repos](/posts/ubuntu-3rd-party)

## (Optional) Wine and 32-bit games support

```bash
sudo dpkg --add-architecture i386
```

## Update your system

```bash
sudo apt update && sudo apt full-upgrade -y
```

## Install regular apps

### Regular Ubuntu

Save this list in `pkgs.txt`

```txt
# Developement
build-essential
git
git-lfs
code

# Network
cifs-utils
deluge

# System
ubuntu-restricted-extras
gnome-shell-extension-manager
parallel
htop
bpytop
baobab
synaptic
apt-xapian-index
neofetch
zsh
ppa-purge

# Locale
ibus
ibus-chewing

# Media
ffmpeg
vlc
mcomix
viewnior

# Themes
# papirus-icon-theme
# qt5-style-kvantum-themes
# qt5-style-kvantum
# qt5ct

# Fonts
fonts-noto
fonts-wqy-microhei
fonts-wqy-zenhei
fonts-open-sans

# Editors
zotero
libreoffice
```

Run the following scripts

```bash
sudo -v
echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | sudo debconf-set-selections
sed 's/#.*$//' pkgs.txt | xargs sudo apt install -y
```

### Kubuntu and KDE Neon

Save this list in `pkgs.txt`

```txt
# Developement
build-essential
git
git-lfs
code

# Network
cifs-utils
qbittorrent

# System
parallel
zsh
htop
bpytop
neofetch
kio-extras
gnome-keyring
kubuntu-restricted-extras
ppa-purge

# Locale
ibus
ibus-chewing

# Media
ffmpeg
smplayer

# Fonts
fonts-noto
fonts-wqy-microhei
fonts-wqy-zenhei
fonts-open-sans

# Editors
zotero
libreoffice
```

Run the following scripts

```bash
sudo -v
echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | sudo debconf-set-selections
sed 's/#.*$//' pkgs.txt | xargs sudo apt install -y
```

## Python APPs

```bash
[[ -x "$(command -v pip)" ]] && pip install -U --user yt-dlp glances
```

You might want to reload `~/.profile` to load them in `PATH`.

```bash
source ~/.profile
```

## Snap apps

```bash
sudo snap install btop && sudo snap connect btop:removable-media
sudo snap install telegram-desktop
sudo snap install hugo --channel=extended/stable
sudo snap install gitkraken --classic
```

## Other configurations

Reduce swap usage

```bash
echo 'vm.swappiness=10' | sudo tee -a /etc/sysctl.conf
```

## Ubuntu: Extensions for gnome shell

From the [gnome shell website](https://extensions.gnome.org/) + browser addon

- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
- [Audio Output Switcher](https://extensions.gnome.org/extension/751/audio-output-switcher/)
- [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)
- [Lock Keys](https://extensions.gnome.org/extension/36/lock-keys/)
- [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/) for a category-based menu for applications.
- [Dash to panel](https://extensions.gnome.org/extension/1160/dash-to-panel/) for a Win-8sque experience.
- [Arc Menu](https://extensions.gnome.org/extension/3628/arcmenu/)
- [Material shell](https://extensions.gnome.org/extension/3357/material-shell/) tiling windows.

## Kubuntu/KDE Neon: System Settings

- Double click to open files instead of single clicks: `Workspace behavior` => `General behavior` => `click behavior`.
- Start with an empty session in `Desktop session`

## Download other apps if needed

- [MarkText](https://github.com/marktext/marktext)
- [FreeFileSync](https://freefilesync.org/)
- [Starship](https://starship.rs/)
- [Hugo](https://github.com/gohugoio/hugo/releases/)
- [Pandoc](https://github.com/jgm/pandoc/releases/)
- [Virtualbox](https://www.virtualbox.org/)
