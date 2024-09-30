[TOC]

# Overview

A computer is a device that can be instructed to carry out an arbitrary
set of arithmetic or logical operations automatically.

# History

## Pre-19th century

- The earliest counting device was probably a form of tally stick.
- The abacus was initially used for arithmetic tasks.
    + The Roman abacus was used in Babylonia as early as 2400 BC.
- The Antikythera mechanism is believed to be the earliest mechanical
  analog "computer." It was designed to calculate astronomical
  positions. It was discovered in 1901 in the Antikythera wreck off the
  Greek island of Antikythera, between Kythera and Crete, and has been
  dated to circa 100 BC.
- The sector, a calculating instrument used for solving problems in
  proportion, trigonometry, multiplication and division, and for various
  functions, such as squares and cube roots, was developed in the late
  16th century and found application in gunnery, surveying, and
  navigation.
- The slide rule was invented around 1620-1630, shortly after the
  publication of the concept of the logarithm. It is a hand-operated
  analog computer for doing multiplication and division. As slide rule
  development progressed, added scales provided reciprocals, squares and
  square roots, as well as transcendental functions such as logarithms
  and exponential, circular, hyperbolic trigonometry, and other
  functions.

## First computing device

- Charles Babbage, an English mechanical engineer and polymath,
  originated the concept of a programmable computer.
- The Analytical Engine. The input of programs and data was to be
  provided to the machine via punched cards, a method being used at the
  time to direct mechanical looms such as the Jacquard loom.
- For output, the machine would have a printer, a curve plotter and a
  bell. The machine would also be able to punch numbers onto cards to be
  read in later.
- The Engine incorporated an arithmetic logic unit, control flow in the
  form of conditional branching and loops, and integrated memory,
  making it the first design for a general-purpose computer that could
  be described in modern terms as Turing-complete.

## Digital computers

### Electromechanical

- The Z2, created by German engineer Konrad Zuse in 1939, was one of the
  earliest examples of an electromechanical relay computer.
- In 1941, Zuse followed his earlier machine up with the Z3, the world's
  first working electromechanical programmable, fully automatic digital
  computer.
    + The Z3 was built with 2000 relays, implementing a 22 bits word
      length that operated at a clock frequency of about 5-10 Hz.
    + Program code was supplied on punched film while data could be
      stored in 64 words of memory or supplied from the keyboard.
    + The Z3 was Turing-complete.

### Vacuum tubes and digital electronic circuits

- In 1943, Max Newman created Colossus, the first electronic digital
  programmable computing device, and it was used to break German ciphers
  during World War II. It used a large number of vacuum tubes. It was
  not Turing-complete.
- In 1946, the U.S. built ENIAC (Electronic Numerical Integrator and
  Computer) was the first electronic programmable computer, Turing-
  complete device. The machine was huge, weighing 30 tons, using 200
  kilowatts of electric power and contained over 18,000 vacuum tubes,
  1,500 relays, and hundreds of thousands of resistors, capacitors, and
  inductors.

## Modern computers

### Concept of modern computer

The principle of the modern computer was proposed by Alan Turing in his
seminal 1936 paper, *On Computable Numbers*.
- Turing proposed a simple device that he called "Universal Computing
  machine" and that is now known as a universal Turing machine.
- He proved that such a machine is capable of computing anything that is
  computable by executing instructions (program) stored on tape,
  allowing the machine to be programmable.
- The fundamental concept of Turing's design is the stored program,
  where all the instructions for computing are stored in memory.
- Von Neumann acknowledged that the central concept of the modern
  computer was due to this paper.
- Turing machines are to this day a central object of study in theory of
  computation.
- Except for the limitations imposed by their finite memory stores,
  modern computers are said to be Turing-complete, which is to say, they
  have algorithm execution capability equivalent to a universal Turing
  machine.

### Stored programs

- Early computing machines had fixed programs. Changing its function
  required the re-wiring and re-structuring of the machine.
- In 1948, the Manchester Small-Scale Experimental Machine (SSEM),
  nicknamed Baby, was the world's first stored-program computer.
- In 1951, the Ferranti Mark 1 was the world's first commercially
  available general-purpose computer.

### Transistors

- The bipolar transistor was invented in 1947. From 1955, transistors
  replaced vacuum tubes in computer designs, giving rise to the "second
  generation" of computers.
- In 1955, the Harwell CADET was the first completely transistorized
  computer.

### Integrated circuits

- The next advance in computing power came with the advent of the
  integrated circuit.
- Geoffrey Dummer presented the first public description of an
  integrated circuit at the Symposium on Progress in Quality Electronic
  Components in Washington, D.C. on 7 May 1952.
- Jack Kilby invented the first working integrated example on 12
  September 1958.
- The first single-chip microprocessor was the Intel 4004.

### Mobile computers

- Portable computers grew in popularity in the 2000s.

# Potential Laptops

- Macbook (using Linux with AsahiLinux - rising sun Linux distro)
    + Air M1 chip
        * 16 GB RAM, 512 GB SSD: 1259 dollars
        * M1 chip is superior than i7, or even i9 since CPU, GPU, RAM are
          all in the same chip tightly integrated.
    + Pro
- Thinkpad
    + X1 Carbon
    + Z16
    + T490
        * 16 GB RAM, 512 GB SSD: 1299 dollars (Costco)
- Dell
    + XPS 13/15
- Starlabs
    + https://us.starlabs.systems/
- System 76:
    + Galapo Pro: 16 GB RAM, 512 GB SSD, i7: 1210 dollars

# Lenovo Thinkpad X220 - 2011

## Resources

- https://www.thinkwiki.org/wiki/Category:X220
- https://wiki.archlinux.org/index.php/Lenovo_ThinkPad_X220
- http://x220.mcdonnelltech.com/dual-boot-one-drive/
- http://x220.mcdonnelltech.com/
- https://wiki.archlinux.org/index.php/Clover
- https://wiki.archlinux.org/index.php/Systemd-boot
    + https://wiki.archlinux.org/index.php/Systemd-boot#EFI_Shells_or_other_EFI_apps
- http://www.rodsbooks.com/efi-bootloaders/
- https://bbs.archlinux.org/viewtopic.php?id=210875
- https://aur.archlinux.org/packages/memtest86-efi/

### Update BIOS

- https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x220/downloads/ds018807
- https://xo.tc/updating-uefi-bios-on-lenovo-thinkpad-x220.html
- https://www.youtube.com/watch?v=jsCfFOywZs0&t=0s&index=7&list=WL

### Dual/Triple Booting

- https://www.howtogeek.com/214571/how-to-dual-boot-linux-on-your-pc/
- https://askubuntu.com/questions/66070/how-to-set-windows-bootloader-as-default-bootloader
- https://wiki.archlinux.org/index.php/Dual_boot_with_Windows/SafeBoot
- https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system
- https://wiki.archlinux.org/index.php/Dual_boot_with_Windows


## Hardware

- Storage
    + Primary: 2.5" SATA III -> a SATA III SSD
        * 500 GB SSD Samsung 850 Evo
    + Secondary: mSATA SSD (Optional)
- RAM
    + supported
        * max 8 GB - DDR3 - 1333 MHz
    + unsupported
        * max 16 GB - DDR3 - 1600/1866 MHz
        * need firmware update or custom firmware
        * careful with firmware update, need research
        * *CHOSE*: 16 GB DDR3 1333 MHz
- CPU
    + i7 2620M - 2.7 GHz - 2 cores - 4 logical processors

## Firmware

- Something

# Lenovo Thinkpad X1 Carbon

- https://wiki.archlinux.org/index.php/Lenovo_ThinkPad_X1_Carbon

# References

[wiki]: https://en.wikipedia.org/wiki/Computer
