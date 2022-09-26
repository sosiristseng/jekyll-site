---
title: "Strip Jupyter Notebook Output"
date: 2022-01-14T13:58:53+08:00
tags: ["jupyter", "python", "git"]
categories: ["Python"]
---

Jupyter notebooks without multimedia outputs are more friendly to source control since git by default does a poor job comparing diffs of binary files (e.g. plots). You can use `nbconvert` to remove the output cells of Jupyter notebooks.

```bash
jupyter nbconvert --clear-output --inplace my_notebook.ipynb
```

<!--more-->

YOu can use Git automation to strip the output automatically on git commit. The following git filter settings keep full notebooks as-is but commit the "clean" version.

In your project folder's `.git/config`:

```gitconfig
[filter "strip-notebook-output"]
    clean = "jupyter nbconvert --clear-output --inplace --stdin --stdout --log-level=ERROR"
```

And in your project folder's `.gitattributes`:

```gitattributes
*.ipynb filter=strip-notebook-output
```

How this works: [^1]

- The `attribute` tells git to run the filter's clean action on each notebook file before adding it to the index (staging).
- The filter is our friend `nbconvert`, set up to read from stdin, write to stdout, strip the output, and only speak when it has something important to say.
- When a file is extracted from the index, the filter's smudge action is run, but this is a no-op as we did not specify it. You could run your notebook here to re-create the output (`nbconvert --execute --inplace`).
- Note that if the filter somehow fails, the file will be staged unconverted.

[^1]: <https://stackoverflow.com/questions/28908319/how-to-clear-jupyter-notebooks-output-in-all-cells-from-the-linux-terminal>

## nbstripout

[`nbstripout`](https://github.com/kynan/nbstripout) is a python package to setup these things above for you.

## nbstripout-fast

[nbstripout-fast](https://github.com/stas00/jupyter-notebook-tools/blob/master/nbstripout/nbstripout-fast) is a simple python script much faster than `nbconvert --clear-output`.

In your project folder's `.git/config`:

```gitconfig
[filter "nbstripout"]
	clean = nbstripout-fast
    # smudge = cat
    # required = true
[diff "ipynb"]
    textconv = nbstripout-fast -t
```

And in your project folder's `.gitattributes`:

```gitconfig
[filter "nbstripout"]
	clean = nbstripout-fast
    # smudge = cat
    # required = true
[diff "ipynb"]
    textconv = nbstripout-fast -t
```

## Alternatives

[`jupytext`](https://github.com/mwouts/jupytext) let one edit and run Jupyter notebooks and save as [paired markdown files](https://github.com/mwouts/jupytext/blob/main/docs/paired-notebooks.md) for source control.
