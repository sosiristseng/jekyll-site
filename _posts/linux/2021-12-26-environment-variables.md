---
title: "Environment Variables"
date: 2021-12-26T14:21:47+08:00
tags: []
categories: ["Linux"]
---

<!--more-->

## Linux

### System-wide

- `/etc/profile` is sourced by all POSIX-compatible shells upon login.
- Files inside the `/etc/profile.d/` directory will also be sourced.

### Bash

- `~/.profile` or `~/.bash_profile` for login bash shells.
- `~/.bashrc` for every bash (login shell) instance.

### Zsh

- `~/.zshenv` for environment variables in zsh.
- `~/.zprofile` for login zsh shells.
- `~/.zshrc` for every zsh (login shell) instance.

⚠️ zsh [does not read](https://superuser.com/questions/187639/zsh-not-hitting-profile) `~/.profile` by default. You can add this line to `~/.zprofile` or `~/.zshenv` to let zsh login shells read `~/.profile`

```bash
[[ -r ~/.profile ]] && emulate sh -c 'source ~/.profile'
```

### X windows

- `~/.xinitrc` is sourced by `startx`.
- `~/.xprofile` is sourced by display managers (e.g. GDM, SDDM)

### Systemd

`~/.config/environment.d/*.conf`: sourced by `systemd`. Used in WayLand sessions where `xinitrc` and `xprofile` is not available.


### See also

- [Arch Wiki: environment variables](https://wiki.archlinux.org/index.php/environment_variables)


## Windows

- [Wikipedia: setx command](https://docs.microsoft.com/zh-tw/windows-server/administration/windows-commands/setx)
- Microsoft docs for [set](https://docs.microsoft.com/zh-tw/windows-server/administration/windows-commands/set_1) and [setx](https://docs.microsoft.com/zh-tw/windows-server/administration/windows-commands/setx)

### Shell variables

Variables created by `set` are bound to the current session and not persistent.

```powershell
set x=123
echo %x%  # You need to wrap the var between % to show the value
```

### Persistent variables

- GUI: Windows Settings -> Advanced system settings -> Set **Environment Variables**.
- CLI: `setx`. See also `setx /?` for complete options.

```powershell
setx <variable> <value>
```
