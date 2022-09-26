---
title: "Conda in Github Actions"
date: 2021-12-26T13:00:54+08:00
tags: ["python", "conda", "github", "github actions", "devops"]
categories: ["Python"]
---

Using [setup miniconda](https://github.com/conda-incubator/setup-miniconda) GitHub Actions.

<!--more-->

## Mambaforge

Using new and fast [mamba](https://github.com/mamba-org/mamba) package manager.

The example workflow file below only shows the `jobs` section.

```yml
jobs:
  mambaforge-example:
    runs-on: "ubuntu-latest"
    defaults: # (2)
      run:
        shell: bash -l {0}
    steps:
      - uses: actions/checkout@v2
      - uses: conda-incubator/setup-miniconda@v2
        with:
          miniforge-variant: Mambaforge  # (1)
          miniforge-version: latest
          environment-file: environment.yml
          use-mamba: true
      - run: |
          conda info
          conda list
      - run: mamba install jupyterlab
```

- (1) : enables `mamba` by specifying `miniforge-variant` as `Mambaforge`.
- (2) : `bash -l {0}` login shell to activate the conda environment correctly.
