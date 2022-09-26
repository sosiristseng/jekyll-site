---
title: "Windows postinstall"
date: 2021-12-25T16:57:01+08:00
tags: ["windows", "postinstall"]
categories: ["Windows"]
---

This to do after Windows install.

<!--more-->

## (Optional) Minimalistic NVidia GPU driver

Use [nvcleaninstall][] to choose the driver components really needed without bloat.[^nvclean]

**Uninstall current GPU drivers (if you already installed one)**

Boot Windows in [safe mode][] and run [display driver uninstaller][].

**Clean install NV driver**

Use [nvcleaninstall][] to install Nvidia driver.

[safe mode]: https://support.microsoft.com/en-us/windows/start-your-pc-in-safe-mode-in-windows-10-92c27cff-db89-8644-1ce4-b3e5e56fe234
[display driver uninstaller]: https://www.guru3d.com/files-details/display-driver-uninstaller-download.html
[nvcleaninstall]: https://www.techpowerup.com/download/techpowerup-nvcleanstall/

[^nvclean]: NV Clean Install's [introduction in Youtube](https://youtu.be/LR1XkjtylCM)

## Chocolatey package manager

Install [Chocolatey 🍫](https://chocolatey.org/), a command-line interface (CLI) package manager for Windows.

Open the powershell prompt with admin privilege (e.g. via the `Windows + X` menu):

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Install my packages

```powershell
choco install -y vscode git gitkraken qbittorrent firefox brave anydesk telegram microsoft-teams peazip bandizip honeyview potplayer yt-dlp ffmpeg crystaldiskinfo directx vcredist140 hugo-extended sudo adobereader starship
```

See the  [🍫 Chocolatey package list](https://chocolatey.org/packages) for additional packages.

## Using winget "official" package manager

Go to <https://winget.run/> and click `Install winget`.

You can also find available packages in <https://winget.run/>.
