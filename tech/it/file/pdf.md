[TOC]

# Overview

# Tips and Tricks

## PDF Utilities


| Program               | Description                                     |
| -                     | -                                               |
| convert (ImageMagick) | Converting images to pdf(s) or pdf(s) to images |
| gs (ghostscript)      | Multiple functions                              |
| pdfunite (poppler)    | Merging pdfs                                    |
| pdfjam (texlive-core) | Merging pdfs                                    |
| pdfimages (poppler)   | Extracting images in pdfs                       |
| pdftk                 | Multiple functions                              |

## Reduce file size

- `ps2pdf LARGE.pdf SMALL.pdf`
- `gs -sDEVICE=pdfwrite -dPDFSETTINGS=/ebook -q -o output.pdf file.pdf`
- `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf`
- Compress pdfs
    + `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf`
    + https://askubuntu.com/questions/113544/how-can-i-reduce-the-file-size-of-a-scanned-pdf-file
    + http://milan.kupcevic.net/ghostscript-ps-pdf/

```
-dPDFSETTINGS=/screen   (screen-view-only quality, 72 dpi images)
-dPDFSETTINGS=/ebook    (low quality, 150 dpi images)
-dPDFSETTINGS=/printer  (high quality, 300 dpi images)
-dPDFSETTINGS=/prepress (high quality, color preserving, 300 dpi imgs)
-dPDFSETTINGS=/default  (almost identical to /screen)
```
- PDF with full color scan images
    + `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dDownsampleColorImages=true \
    -dColorImageResolution=150 -dNOPAUSE  -dBATCH -sOutputFile=output.pdf input.pdf`
- `convert -compress Zip -density 150x150 input.pdf output.pdf`

## Removing password

**The easiest way GUI** (recommended for novice)

Open the protected file and use <kbd>ctrl</kbd>+<kbd>p</kbd> or use print option to print the file, now save the file as pdf.

<hr>

**Using Command line**

If you have pdftk already installed you can skip step1

Step 0: To check if Pdftk is already installed

    sudo apt list | grep pdftk

If output contains '[installed]' tag with pdftk then you can skip step1
i.e if the output is like this

    pdftk/xenial 2.02-4 amd64 [installed]

Step 1: Install pdftk

    sudo apt-get install pdftk

Step 2: Run following command

    pdftk /path/to/input.pdf input_pw <yourpassword> output out.pdf

<hr>
If you don't want to install pdftk there is another utility qpdf which is automatically installed (at least on 16.04 which I am using)

To use qpdf for generating unsecured pdf run following command.

    qpdf -password=<your-password> -decrypt /path/to/secured.pdf out.pdf

For detailed information take a look at [this][1] HTG tutorial


  [1]: http://www.howtogeek.com/197195/how-to-remove-a-password-from-a-pdf-file-in-linux/
