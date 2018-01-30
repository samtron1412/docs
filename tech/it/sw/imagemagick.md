[TOC]

# Overview

ImageMagick is a free software suite for the creation, modification and
display of bitmap images.

# Utilities

## convert

Convert between image formats as well as resize an image, blur, crop,
despeckle, dither, draw on, flip, join, re-sample, and much more.

### Convert pdf to images

| Command                                                                | Description                                                         |
| -                                                                      | -                                                                   |
| `convert input.pdf output.pdf`                                         | pdf to images                                                       |
| `convert input.pdf[1] output.pdf`                                      | a particular page to an image                                       |
| `convert -verbose -density 300 input.pdf -quality 100 output.jpg`      | a better quality for text using -density 300                        |
| `convert -verbose -density 300 input.pdf -quality 100 output-%02d.jpg` | formatting the output filename with two digits (e.g. output-01.jpg) |

### Convert images to pdf

https://stackoverflow.com/questions/2507766/merge-convert-multiple-pdf-files-into-one-pdf

| Command                    | Description                     |
| `convert *.jpg output.pdf` | multiple images to one pdf file |

```bash
# Convert images to pdf with same size
# If the output images wrong direction, erase rotate 90
convert -rotate 90 a.png b.png -compress jpeg -resize 1240x1753 \
    -extent 1240x1753 -gravity center \
    -units PixelsPerInch -density 150x150 multipage.pdf

convert -compress jpeg -units PixelsPerInch -density 150x150 -rotate 90 tax-return-2016.JPG tax.pdf

https://unix.stackexchange.com/questions/20026/convert-images-to-pdf-how-to-make-pdf-pages-same-size
```

## identify

Describes the format and characteristics of one or more image files.

## mogrify

Like convert, but mogrify overwrites the original image file, whereas,
convert writes to a different image file.

## composite

Overlaps one image over another.

## montage

Create a composite image by combining several separate images.

## compare

Mathematically and visually annotake the difference between an image and
its reconstruction.

## stream

It is a lightweight tool to stream one or more pixel components of the
image or portion of the image to your choice of storage formats. It
writes the pixel components as they are read from the input image a row
at a time making stream desirable when working with large images or when
you require raw pixel components.

## display

Displays an image or image sequence on any X server.

## animate

Animates an image sequence on any X server.

## import

Saves any visible window on an X server and outputs it as an image file.
You can capture a single window, the entire screen, or any rectangular
portion of the screen.

## conjure

Interprets and executes scripts written in the Magick Scripting Language
(MSL).
