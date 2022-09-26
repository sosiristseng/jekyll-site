---
title: "Endeavour OS Postinstall"
date: 2021-12-26T15:19:23+08:00
tags: ["postinstall", "endeavour os"]
categories: ["Linux"]
---

Things to do for installing [endeavour OS](https://endeavouros.com/).

<!--more-->

## Custom packages for installer

[Add custom additional (non-AUR) packages to the installer](https://discovery.endeavouros.com/installation/add-packages-to-be-installed-in-addition-to-desktop-chosen/2021/04/) by adding packages to `~/user_pkglist.txt`.

Common packages

```txt
akm
base-devel
python-pip
python-virtualenv
python-setuptools
python-wheel
git
git-lfs
libreoffice-fresh
hugo
vivaldi
vivaldi-ffmpeg-codecs
telegram-desktop
btop
zsh
docker
parallel
trash-cli
ffmpeg
yt-dlp
virtualbox
virtualbox-host-dkms
virtualbox-guest-iso
gnome-keyring
ttf-roboto
noto-fonts
noto-fonts-cjk
noto-fonts-emoji
wqy-microhei
wqy-zenhei
ttf-opensans
ibus
ibus-chewing
```

### KDE

Packages specifically for the KDE edition:

```txt
qbittorrent
ksysguard
partitionmanager
kdialog
xdg-desktop-portal-kde
xdg-desktop-portal
plasma-systemmonitor
kdeplasma-addons
krename
ffmpegthumbs
```

### XFCE

Packages specifically for the XFCE edition:

```txt
deluge-gtk
celluloid
gparted
qt5ct
kvantum
kvantum-theme-materia
materia-gtk-theme
papirus-icon-theme
viewnior
mcomix
xreader
```

## Custom commands for the installer

[Add custom commands for the installer](https://endeavouros.com/latest-release/) by editing `~/user_commands.bash`.

### KDE

```bash
#!/bin/bash
pacman -Rns ffmpegthumbnailer --noconfirm

# Activate services
systemctl enable docker.service
username=$(cat /tmp/new_username.txt)
usermod -aG docker $username
usermod -aG vboxusers $username

# Reduce swapiness
echo vm.swappiness=10 | tee /etc/sysctl.d/99-swappiness.conf
```

### XFCE

```bash
# Activate services
systemctl enable docker.service
username=$(cat /tmp/new_username.txt)
usermod -aG docker $username
usermod -aG vboxusers $username

# Reduce swapiness
echo vm.swappiness=10 | tee /etc/sysctl.d/99-swappiness.conf
```

## After install: Select fastest mirror

Click `select mirror` in the welcome APP, run the speed test, and save the mirror list.

## Set yay options

```bash
yay --answerclean All --answerdiff None --answerupgrade None --cleanafter --batchinstall --combinedupgrade --sudoloop --save
```

> The options `--answerdiff None` and `--answerupgrade None` might be controversial since they skip manual `PKGBUILD` checks.

## (Optional) Install other AUR helpers

EnOS installs `yay` AUR helper by default. If you want other [AUR helpers](https://wiki.archlinux.org/title/AUR_helpers), install them via `yay`.

```bash
# pikaur
yay -S pikaur
# paru
yay -S paru
```

## Install AUR packages

```bash
yay -S  gitkraken \
        visual-studio-code-bin \
        tectonic-bin \
        pandoc-bin \
        zotero-bin \
        brave-bin \
        snapper-support \
        nerd-fonts-fira-code \
        nerd-fonts-hack \
        virtualbox-ext-oracle \
        freefilesync-bin
```

## Set Environment Variables

Append the following lines to `~/.profile`

```bash
test -d "${HOME}/.local/bin" && PATH="${HOME}/.local/bin:${PATH}"
test -d "${HOME}/.cargo/bin" && PATH="${HOME}/.cargo/bin:${PATH}"
test -d "${HOME}/go/bin"     && PATH="${HOME}/go/bin:${PATH}"

export BROWSER=$(command -v xdg-open)
export EDITOR=$(command -v nano)
```

## NVIDIA GPU

To install the Nvidia GPU driver and the GUI control panel

```bash
sudo pacman -S nvidia-dkms nvidia-settings
```

### CUDA runtime

```bash
sudo pacman -S cuda cudnn
```

### Docker containers with CUDA support

```bash
yay -S nvidia-container-toolkit
sudo systemctl restart docker
```

### (Optional) Dual boot

```bash
sudo pacman -S os-prober
```

Open `/etc/default/grub` and edit/add the following lines

```
GRUB_DISABLE_OS_PROBER=false
```

Afterwards, run

```bash
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

to apply GRUB options

## KDE-specific tweaks

### Power profiles

Enable power profiles service to switch between energy-saving/power modes

```bash
sudo pacman -S power-profiles-daemon
sudo systemctl enable --now power-profiles-daemon.service
```

### Bluetooth

```bash
sudo pacman -S bluez-utils bluedevil
sudo rfkill unblock bluetooth
sudo systemctl enable bluetooth
```

### Firewall

```bash
sudo pacman -S ufw plasma-firewall
sudo systemctl enable --now ufw.service
sudo ufw enable
sudo systemctl enable ufw
```

### Disable Baloo File Indexer

```bash
sudo balooctl suspend && sudo balooctl disable
```

### Improve shutdown reboot time in KDE systems

```bash
# Create a script to kill KWin
sudo tee /usr/lib/systemd/system-shutdown/kill_kwin.shutdown << END
#!/bin/sh

# Kill KWin immediately to prevent stalled shutdowns/reboots
pkill -KILL kwin_x11
END
sudo chmod +x /usr/lib/systemd/system-shutdown/kill_kwin.shutdown

# Create a systemd unit to run the script
sudo tee /etc/systemd/system/kill_kwin.service << END
[Unit]
Description=Kill KWin at shutdown/reboot

[Service]
Type=oneshot
ExecStart=/bin/true
ExecStop=/bin/sh /usr/lib/systemd/system-shutdown/kill_kwin.shutdown
RemainAfterExit=true

[Install]
WantedBy=multi-user.target
END

sudo systemctl enable --now kill_kwin.service
```

## XFCE-specific tweaks

### Themes

Settings Manager:
- Apperance (for window contents)
  - Style: Materia-compact
  - Icons: Papirus
  - Fonts: Roboto Medium 10.5 pts
- Kvantum manager: Use Materia-compact
- Windows manager (for window borders):
  - Style: Theme `Materia-compact` and title font `Roboto Black` 10.5 pts
  - Advanced -> Windows snapping: check `To other windows`

QT5 settings:
- Style: Kvantum
- Fonts: Roboto 11pt
- Icon theme: papirus
- Stylesheets: deselect all

### Hotkeys

Settings Manager:
- Keyboard
  - Application shortcuts: change shortcuts for `xfce4-popup-whiskermenu`, etc.

### Password storage

Settings Manager:
- Session and startup
  - Advanced: Launch GNOME services on startup

## Additional packages

`yay -S <pkgname>`

- [PyCharm](https://www.jetbrains.com/pycharm/): `pycharm-community-jre`
- Java runtime: `jre-openjdk`
- Google drive client: `google-drive-ocamlfuse-opam`
- Onedrive client: `onedrive-abraunegg`

## Sources

- [EndeavourOS wiki](https://discovery.endeavouros.com/wiki/)
- [ArchLinux Wiki](https://wiki.archlinux.org/)
- [Reddit: Average User's To Do List after doing a fresh install of Endeavour OS with KDE Plasma](https://www.reddit.com/r/EndeavourOS/comments/rbdlhw/atlantis_edition_average_users_to_do_list_after/)
- [Reddit: Fix for slow shutdown and reboot on Manjaro KDE and other Arch based distrubutions with a KDE DE](https://www.reddit.com/r/ManjaroLinux/comments/oq2aez/fix_for_slow_shutdown_and_reboot_on_manjaro_kde/)
