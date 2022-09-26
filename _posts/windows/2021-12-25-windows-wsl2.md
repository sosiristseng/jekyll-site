---
title: "Windows subsystem for Linux 2 (WSL2)"
date: 2021-12-25T16:59:31+08:00
tags: ["windows", "linux", "wsl2"]
categories: ["Windows"]
---

Setup Windows subsystem for Linux 2 (WSL2)[^1] for Linux developement experience in Windows 10 and 11.

<!--more-->

## One command install

In recent versions of Windows 10/11, open powershell with administrator privileges, run[^2]:

```powershell
wsl --install
```

<!--more-->

This command will:
- Enable virtulization platform (Hyper-V).
- Install Windows subsystem for Linux (WSL2 by default).
- Install the latest Ubuntu LTS as a Windows App.


[^1]: https://docs.microsoft.com/en-us/windows/wsl/
[^2]: https://devblogs.microsoft.com/commandline/install-wsl-with-a-single-command-now-available-in-windows-10-version-2004-and-higher/

## Running GUI Apps

Currently, Windows 11 is needed to enable [WSLg](https://github.com/microsoft/wslg) support. Once WSL2 is installed successfully, `WSLg` is enabled by default and you can [install and run](https://github.com/microsoft/wslg#install-and-run-gui-apps) Linux GUI apps. [Install GPU drivers](https://github.com/microsoft/wslg#pre-requisites) for better performance.

You might want to update WSL kernel version (with administrator privileges):

```powershell
wsl --update
```

## Configure WSL2

In your windows home directory (`%USERPROFILE%` folder) configure the file `.wslconfig`.[^wslconfig]

```
[wsl2]
kernel=<path>              # An absolute Windows path to a custom Linux kernel.
memory=<size>              # How much memory to assign to the WSL2 VM.
processors=<number>        # How many processors to assign to the WSL2 VM.
swap=<size>                # How much swap space to add to the WSL2 VM. 0 for no swap file.
swapFile=<path>            # An absolute Windows path to the swap vhd.
localhostForwarding=<bool> # Boolean specifying if ports bound to wildcard or localhost in the WSL2 VM should be connectable from the host via localhost:port (default true).
kernelCommandLine = <string> # Additional kernel command line arguments

# <path> entries must be absolute Windows paths with escaped backslashes, for example C:\\Users\\Ben\\kernel
# <size> entries must be size followed by unit, for example 8GB or 512MB
```

[^wslconfig]: https://docs.microsoft.com/en-us/windows/wsl/release-notes#build-18945

## Caveats

### Poor filesystem performance across OS boundaries

For example, Windows I/O accessing into WSL and WSL accessing `/mnt/c/` will results in translations between two different file systems (NTFS vs ext4) and thus pooror performance.

To have a better disk I/O performance, run WSL jobs inside WSL's own filesystem and vice versa where I/O speed is important (e.g. git, database).
