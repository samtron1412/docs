[TOC]

# Overview

# Tips and Tricks

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
