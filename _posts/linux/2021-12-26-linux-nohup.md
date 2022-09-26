---
title: "Nohup: do not hang up in SSH sessions"
date: 2021-12-26T14:45:29+08:00
tags: ["ssh"]
categories: ["Linux"]
---

<!--more-->

`nohup` can run background process(es) uninterruptedly even a remote SSH session is offline.

```bash
nohup mycmd &
```

## Output

The output will be in `nohup.out` by default. If you want to customize the output location, just redirect it:

```bash
nohup mycmd &> log.txt &
```

You can also lower the priority for the background process

```bash
nohup nice mycmd &
```

## End process

When you're done, you can kill the process by the proccess ID (PID)

```bash
ps -aux | grep mycmd

kill PID
```

## Sources

- [GT Wang](https://blog.gtwang.org/linux/linux-nohup-command-tutorial/)
