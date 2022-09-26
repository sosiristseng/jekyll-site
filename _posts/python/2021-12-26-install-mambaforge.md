---
title: "Install Mambaforge"
date: 2021-12-26T13:34:59+08:00
tags: ["python", "conda", "mamba"]
categories: ["Python"]
---

How to install mambaforge: the community-driven [conda-forge](https://github.com/conda-forge/miniforge) repo with fast new [mamba](https://github.com/mamba-org/mamba) package manager.

<!--more-->

## Install mamba-forge on Windows

Download and run the installer from the [miniforge GitHub repo](https://github.com/conda-forge/miniforge#mambaforge).

## Install mamba-forge on Linux

The following script to

- Install mambaforge: [miniforge](https://github.com/conda-forge/miniforge) plus [mamba](https://github.com/mamba-org/mamba) package manager.
- Integration with `bash` and `zsh` shells if available.

```bash
CONDA_PATH="${HOME}/conda"
CONDA_SH="${CONDA_PATH}/etc/profile.d/conda.sh"
CONDA_URL="https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Linux-x86_64.sh"

# Download and install miniconda
wget -O /tmp/conda.sh "${CONDA_URL}"
bash /tmp/conda.sh -bup "${CONDA_PATH}"

source "${CONDA_SH}"
conda activate base

# conda package manager setup
# conda config --set auto_activate_base false
conda config --set default_threads $(nproc)
mamba update python conda --yes
mamba update --all --yes

# `bash` and `zsh` integration
[[ -f ~/.bashrc ]] && mamba init bash
[[ -f ~/.zshrc ]] && mamba init zsh
```
