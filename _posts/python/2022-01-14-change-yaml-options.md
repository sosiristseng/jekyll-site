---
title: "Change yaml options on-the-fly"
date: 2022-01-14T14:38:43+08:00
tags: ["python", "jupyter-book", "SSG", "yaml"]
categories: ["Python"]
---

Jupyter book settings are defined in `_config.yml`; however, you can customize it on-the-fly using the `yaml` module to read and write `_config.yml`.

<!--more-->

```bash
python - <<-EOF
    import yaml
    with open('_config.yml') as f:
        data = yaml.safe_load(f)

    data['execute']['execute_notebooks'] = 'off'

    with open('_config.yml', 'w') as f:
        yaml.dump(data, f)
EOF
```

## Source

- [Stackoverflow: Executing multi-line statements in the one-line command-line](https://stackoverflow.com/questions/2043453/executing-multi-line-statements-in-the-one-line-command-line)
- [Stackoverflow: How to access & modify the content of yaml file from python](https://stackoverflow.com/questions/44418066/how-to-access-modify-the-content-of-yaml-file-from-python)
