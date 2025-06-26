---
layout: single
title: "QR Code Generator Project"
categories: project
tags: [qr-code-generator]
author_profile: false
search: true
---

[GitHub Repository](https://github.com/HenryChung98/qrCodeGenerator)

### Programming Language

- Python

### Introduction

QR code is a two-dimensional barcode made of black squares on a white grid. It was invented in 1994 by Denso Wave for tracking automotive parts.

Using Python's `qrcode` module, you can easily generate QR codes.

### Installation

```bash
pip install qrcode[pil]
```

### Code

```python
import qrcode

data = input('Enter data to encode: ')
version = int(input('Enter version (1-3): '))
box_size = int(input('Enter box size (1-10): '))

qr = qrcode.QRCode(
    version=version,
    box_size=box_size,
    border=5
)

qr.add_data(data)
qr.make(fit=True)

img = qr.make_image(fill_color='black', back_color='white')

filename = input('Enter filename to save (without extension): ')
img.save(f'{filename}.png')

print('QR code generated and saved.')
```
> Note: Version should not be greater than 3 to avoid errors.