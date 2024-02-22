---
layout: single
title: "QR Code Generator"
categories: project
tags: [python, qr-code-generator]
author_profile: false
search: true
---

[my github repo](https://github.com/HenryChung98/qrCodeGenerator)

### Introduction

QR code (Quick Response code) is a two-dimensional barcode that consists of black squares arranged on a white square grid. QR codes were originally created in 1994 by a Japanese company called Denso Wave for tracking automotive parts during the manufacturing process.

Using Python packages like qrcode, pyqrcode modules we can generate and read the QR codes.

Before we start, we need to install two modules:
qrcode (pip3 install QRcode)
image (pip3 install image)

and need to import qrcode

```python
import qrcode
```

### code

To generate QR code, need 3 values:
data: To encode into the QR code.

version: Determines the size and complexity of the QR code.

box size: Represents the size of each module (black square) in the QR code.

#### input

```python
data = input('Enter the Data: ')
version=int(input('Enter the version (complexity): '))  # from 1 to 15
boxSize=int(input('Enter the Box size: '))  # from 1 to 10
```

#### creating qrcode

Now, ready to create an instance of qrcode class

```python
# Creating an instance of QRCode class
qr = qrcode.QRCode(version ,boxSize, border = 5)

# Adding data to the instance 'qr'
qr.add_data(data)

qr.make(fit = True)

# ready to generate the code as an image
img = qr.make_image(fill_color = 'black',back_color = 'white')
```

#### create image file of qrcode

Almost done, now just need to create the image file of the qrcode.

```python
f=input("name it as: ") #image name

img.save(f'{f}.png')

print('qr code generated and saved in the gallery')
```

#### fixed

the size is not allowed greater than 3
