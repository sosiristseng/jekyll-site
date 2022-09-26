---
title: "Command Line Tricks"
date: 2021-12-26T14:07:16+08:00
tags: ["command line"]
categories: ["Linux"]
---

<!--more-->

## Passing arguments to a command from a text file

Using `sed` and `xargs` to pass a list of arguments from a text file

For example, to install two lists of packages in Ubuntu:

```bash
cat list1.txt list2.txt | sed 's/#.*$//' | xargs sudo apt install
```

- `xargs` takes the output from `sed` as arguments to `apt`
- `sed 's/#.*$//'` filters out those lines after `#`. So the `list2.txt` can have comments like this

```txt
# Comment

item1
item2  # A comment after an item
    item3  # indent supported
```

## Passing multiple lines of string

Use heredoc to pass the string as-is between two delimiters (e.g. `EOF`)

```bash
cat << "EOF" >> ~/.xprofile
# ~/.xprofile
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
ibus-daemon -drx
EOF
```

Will append the following lines in `~/.xprofile`:

```bash
# ~/.xprofile
export GTK_IM_MODULE=ibus
export QT_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
ibus-daemon -drx
```
