---
title: "Recover Nautilus Places Folders"
date: 2022-04-15T10:32:13+08:00
tags: ["ubuntu"]
categories: ["Linux"]
---

Recover Nautilus (File manager in Gnome) places folders. [^1]

<!--more-->

![](https://user-images.githubusercontent.com/40054455/163508819-5e853b38-4131-44f1-b1ff-5f116d850e17.png)

Check `~/.config/user-dirs.dirs` and make sure these entries exist

```bash
XDG_DESKTOP_DIR="$HOME/Desktop"
XDG_DOWNLOAD_DIR="$HOME/Downloads"
XDG_DOCUMENTS_DIR="$HOME/Documents"
XDG_MUSIC_DIR="$HOME/Music"
XDG_PICTURES_DIR="$HOME/Pictures"
XDG_VIDEOS_DIR="$HOME/Videos"
```

If they are good, run the following command to recover them.

```bash
xdg-user-dirs-gtk-update
```

[^1]: https://stackallflow.com/ubuntu/how-to-restore-a-places-folder-i-accidentally-deleted-in-nautilus/
