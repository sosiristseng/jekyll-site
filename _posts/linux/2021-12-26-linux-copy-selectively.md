---
title: "Selectively Copy files"
date: 2021-12-26T13:59:15+08:00
tags: ["command line", "tar", "rsync"]
categories: ["Linux"]
---

How to exclude some files/folders while copying a folder tree.

<!--more-->

## Tar

To start with, `tar` and pipes can be used to copy directoy trees[^1]

```bash
tar cf - $src | tar xvf - -C $dst
```

[^1]: https://docstore.mik.ua/orelly/unix3/upt/ch10_13.htm

A filter `.tarignore` excludes files/directories just like `.gitignore` does.[^2][^3]

```bash
tar -c -X .tarignore -f - srcfolder | tar xvf - -C dstfolder
```

Annd the syntax is similar:

```txt
.DS_Store
.git
.gitignore
```

[^2]: https://stackoverflow.com/questions/39514510/exclude-directories-from-tar-archive-with-a-tarignore-file
[^3]: https://www.gnu.org/software/tar/manual/html_node/exclude.html#index-exclude_002dignore


## rsync

Use `--exclude` flag in `rsync` to exclude certain folder(s). [^4]

```bash
rsync -av --progress sourcefolder /destinationfolder --exclude thefoldertoexclude --exclude anotherfoldertoexclude
```

Note: The excluded directory paths are relative to the *sourcefolder*.


[^4]: https://stackoverflow.com/questions/4585929/how-to-use-cp-command-to-exclude-a-specific-directory
