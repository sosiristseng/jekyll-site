---
title: "Fonts Setup"
date: 2021-12-26T13:54:27+08:00
tags: ["fonts"]
categories: ["Linux"]
---

Install custom fonts in Linux systems and make the system recognize it using `fc-cache`.

**Per user**

Copy the font files to `~/.local/share/fonts/`. Then, run `fc-cache` to rebuild the font cache.

```bash
fc-cache -fv
```

**System-wide**

Copy the font files to `/usr/share/fonts/`. Then, run `fc-cache` with admin rights to rebuild the font cache.

```bash
sudo fc-cache -fv /usr/share/fonts/
```

<!--more-->
