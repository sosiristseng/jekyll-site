---
title: "Copy files over SSH"
date: 2021-12-26T14:44:07+08:00
tags: ["ssh"]
categories: ["Linux"]
---

Some Secure shell (SSH) tricks.

<!--more-->

## Using scp command

`scp` works similar to regular copy (`cp`) command

```bash
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

## Using tar and pipe

```bash
tar cvf - $localdir | ssh someone@somemachine '(cd somewhere && tar xBf -)'
```

## Secure FTP (SFTP)

[Filezilla](https://filezilla-project.org/) could access remote servers via the Secure FTP (SFTP) protocol.

And newer versions of `scp` also use `sftp` by default.[^scpandsftp]

[^scpandsftp]: https://wiki.archlinux.org/title/SCP_and_SFTP

## Mount as a disk using sshfs

[sshfs](https://github.com/libfuse/sshfs) could mount remote machine as a local disk via SSH.

```bash
sshfs [user@]hostname:[directory] mountpoint
```

to unmount the disk

```bash
fusermount -u mountpoint
```
