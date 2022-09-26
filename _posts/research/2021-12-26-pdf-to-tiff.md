---
title: "Convert PDF to Tiff"
date: 2021-12-26T00:51:58+08:00
tags: ["pdf", "tiff", "research"]
categories: ["Apps"]
---

Convert `pdf` files to `tiff` images with `pdftoppm` or `ghostscript`.

<!--more-->

## Use pdftoppm

The `pdftoppm` (a part of `poppler-utils`) tool requires less setup than `ghostscript` + `imagemagick` do. [^2][^3]

[^2]: https://www.linuxuprising.com/2019/03/how-to-convert-pdf-to-image-png-jpeg.html
[^3]: https://jdhao.github.io/2019/11/14/convert_pdf_to_images_pdftoppm/

### Install

**Ubuntu**

```bash
sudo apt install poppler-utils
```

**Arch Linux**

```bash
sudo pacman -S poppler-utils
```

**Conda**

```bash
conda install -c conda-forge poppler
```

The windows version of `pdftoppm` provided by conda-forge channel might not be able to convert pdf files to tiff images. Checkout `pdftoppm -h` for available formats.

### Usage

[Documentation of `pdftoppm`](https://www.mankier.com/1/pdftoppm)

For example, to convert the pdf file to a 300-DPI TIFF image with lzw compression.

```bash
pdftoppm -tiff -tiffcompression lzw -r 300 in.pdf outname
```

## Use GhostScript and ImageMagick

### Install

**Ubuntu**

```bash
sudo apt install ghostscript imagemagick
```

### Enable pdf permission

For security reasons, PDF read/write are disable by default. You could change the settings file to fix that.[^1]

[^1]: <https://stackoverflow.com/questions/52998331/imagemagick-security-policy-pdf-blocking-conversion>

`/etc/ImageMagick-7/policy.xml`

```xml /etc/ImageMagick-7/policy.xml
<policy domain="coder" rights="read | write" pattern="PDF" />
```

### Convert pdf to tiff

```bash
convert -density 300 \
        -compress lzw \
        -background white \
        -alpha remove \
        -trim \
        "image.pdf" "image_%d.tiff"
```
