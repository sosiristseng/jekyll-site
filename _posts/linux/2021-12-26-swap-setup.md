---
title: "Swap Setup"
date: 2021-12-26T14:46:59+08:00
tags: ["swap"]
categories: ["Linux"]
---

Swap partition/file setup.

<!--more-->

## Reduce Swapiness

To reduce swap partition/file writes and keep more data in RAM. [@dotblogs](https://dotblogs.com.tw/grayyin/2018/01/10/135915)

```bash
echo 'vm.swappiness = 10' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p            # you should see 'vm.swappiness = 10'
```

## Use Swap file

More flexibility in disk space and partition than swap partitions. Ubuntu installations use swap files by default.

```bash
# Make a 512 MB swapfile.
sudo dd if=/dev/zero of=/swapfile bs=1M count=512
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

Afterwards add the following line to `/etc/fstab`.

```txt
/swapfile none swap defaults 0 0
```
