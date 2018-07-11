[TOC]

# Computer Fonts

>A **computer font** (or font) is an electronic data file containing a
>set of [glyphs](https://en.wikipedia.org/wiki/Glyph), characters, or
>symbols such as [dingbats](https://en.wikipedia.org/wiki/Dingbat).
>Although the term font first referred to a set of metal type sorts in
>one style and size, since the 1990s it is generally used to refer to a
>scalable set of digital shapes that may be printed at many different
>sizes.

There are three basic kinds of computer fonts file data formats:

- **Bitmap** fonts consist of a matrix of dots or
  [pixels](https://en.wikipedia.org/wiki/Pixel) representing the image
  of each glyph in each face and size.
- **Outline** fonts (**vector** fonts) use [Bézier
  curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve), drawing
  instructions and mathematical formulae to describe each glyph, which
  make the character outlines scalable to any size. The universal
  standard was (and still is) Adobe
  [PostScript](https://en.wikipedia.org/wiki/PostScript). Examples are
  PostScript [Type 1 and Type
  3](https://en.wikipedia.org/wiki/Type_1_and_Type_3_fonts) fonts,
  [Truetype](https://en.wikipedia.org/wiki/TrueType) font (ttf) and
  [OpenType](https://en.wikipedia.org/wiki/OpenType) font (otf).
- **Stroke** fonts use a series of specified lines and additional
  information to define the profile, or size and shape of the line in a
  specific face, which together describe the appearance of the *glyph*.

Bitmap fonts are *faster and easier* to use in computer code, but *non-
scalable*, requiring a separate font for each size. Outline and stroke
fonts can be resized using a single font and substituting different
measurements for components of each glyph, but are somewhat more
complicated to render on screen than bitmap fonts, as they require
additional computer code to render the outline to a bitmap for display
on screen or in print. Although all types are still in use, most fonts
seen and used on computers are *outline fonts*.

A raster image can be displayed in a different size only with some
distortion, but renders quickly; outline or stroke image formats are
resizable but take more time to render as pixels must be drawn from
scratch each time they are displayed.

Fonts can be [monospaced](https://en.wikipedia.org/wiki/Monospaced_font)
(i.e., every character is plotted a constant distance from the previous
character that it is next to, while drawing) or proportional (each
character has its own width). However, the particular font-handling
application can affect the spacing, particularly when doing [justificati
on](https://en.wikipedia.org/wiki/Justification_(typesetting)).

## Outline Font Formats

### Type 1 and Type 3 fonts

>[Type 1 and Type 3](https://en.wikipedia.org/wiki/Type_1_and_Type_3_fonts) fonts were developed by Adobe for professional digital typesetting. Using [PostScript](https://en.wikipedia.org/wiki/PostScript), the glyphs are outline fonts described with cubic [Bézier curves](https://en.wikipedia.org/wiki/B%C3%A9zier_curve). Type 1 fonts were restricted to a subset of the PostScript language, and used Adobe's hinting system, which used to be very expensive. Type 3 allowed unrestricted use of the PostScript language, but didn't include any hint information, which could lead to visible rendering artifacts on low-resolution devices (such as computer screens and dot-matrix printers).

### TrueType font

>[TrueType](https://en.wikipedia.org/wiki/TrueType) is a font system originally developed by Apple Inc. It was intended to replace Type 1 fonts, which many felt were too expensive. Unlike Type 1 fonts, TrueType glyphs are described with quadratic Bezier curves. It is currently very popular and implementations exist for all major operating systems.

### OpenType font

>[OpenType](https://en.wikipedia.org/wiki/OpenType) is a smartfont system designed by Adobe and Microsoft. OpenType fonts contain outlines in either the TrueType or Type 1 (actually CFF) format together with a wide range of metadata.

## Stroke font formats

>[METAFONT](https://en.wikipedia.org/wiki/METAFONT) uses a different sort of glyph description. Like TrueType, it is a vector font description system. It draws glyphs using strokes produced by moving a polygonal or elliptical pen approximated by a polygon along a path made from cubic Bézier splines and straight line segments, or by filling such paths. Although when stroking a path the envelope of the stroke is never actually generated, the method causes no loss of accuracy or resolution.

# TeX Fonts

>We will consider three components: Font famillies, Emphasizing text, Font encoding.

## Intro

>[History](https://en.wikipedia.org/wiki/Adobe_Font_Metrics "Adobe Font Metrics")

Originally TeX was used its own *font system* **MetaFont**, designed by
D. Knuth. The default *font family* is **Computer Modern**.

There are many different font types, such as PostScript *Type1/Type3*
fonts and *bitmap* fonts. *Type1* are outline fonts (*vector graphics*)
which are common used by *pdftex*. *Type3* is a superset of Type1 and
has more functionalities from Postscript, such as embedding raster
graphics. In the TeX world, Type3 fonts are often used to embed bitmap
fonts.

The most popular font systems as of this day are
[Truetype](https://en.wikipedia.org/wiki/TrueType) font (ttf) and
[OpenType](https://en.wikipedia.org/wiki/OpenType) font (otf).

## Font families

>There are many font families e.g. Computer Modern, Times, Arial and
>Courier. Those families can be grouped into three main categories:
>roman (rm) or serif, sans serif (sf) and monospace (tt) (see
>[Typeface](https://en.wikipedia.org/wiki/Typeface) for more details).
>Computer Modern Roman is the default font family for LaTeX. Fonts in
>each family also have different properties (size, shape, weight, etc.).
>Families are meant to be consistent, so it is highly discouraged to
>change fonts individually rather than the whole family.

The three families are defined by their respective variables:

- `\rmdefault`
- `\sfdefault`
- `\ttdefault`

Change the family default font:

`\renewcommand*\rmdefault{<font_family_name>}`

Some popular font family name and font name default:

```
Family                 Font Name
--------------------------------------------------
pag                    Avant Garde
fvs                    Bitstream Vera Sans
pbk                    Bookman
bch                    Charter
ccr                    Computer Concrete
cmr                    Computer Modern
pcr                    Courier
mdugm                  Garamond
phv                    Helvetica
fi4                    Inconsolata
lmr                    Latin Modern
lmss                   Latin Modern Sans
lmtt                   Latin Modern Typewriter
LinuxBiolinumT-OsF     Linux Biolinum (formerly 'fxb' in older package versions)
LinuxLibertineT-OsF    Linux Libertine (formerly 'fxl' in older package versions)
pnc                    New Century Schoolbook
ppl                    Palatino
ptm                    Times
uncl                   Uncial
put                    Utopia
pzc                    Zapf Chancery
```

The default family is contained in the `\familydefault` variable, and it
is meant to have one of the three aforementioned variables as value. The
default is defined like the following assignment:

`\renewcommand*{\familydefault}{\sfdefault}`

## Emphasizing Text

>In order to add some emphasis to a word or a phrase, the simplest (and
>the most correct) way is to use the `\emph{text}` command.

## Font encoding

>A *character* is a sequence of bytes, and should not be confused with
>its representation, the *glyph*, which is what the reader sees. So the
>character 'a' has different representations following the used font,
>for example the upright version, the italic version, various weights
>and heights, and so on.

Upon compilation, tex will have to choose the right font glyph for every
character. This is what is called *font encoding*. The default LaTeX
font encoding is OT1, the encoding of the original Computer Modern TeX
text fonts. It contains only 128 characters, many from ASCII, but
leaving out some others and including a number that are not in ASCII.

The `fontenc` package tells LaTeX what font encoding to use. Font
encoding is set with:

`\usepackage['encoding']{fontenc}`

## Font styles

>Each family has its own font characteristics (such as italic and bold), also known as font styles, or font properties.

### Shapes

### Sizing text

>`{\Large some words}`

`\tiny`
`\scriptsize`
`\footnotesize`
`\small`
`\normalsize`
`\large`
`\Large`
`\LARGE`
`\huge`
`\Huge`

## Local font selection

>You can change font for a specific part of the text. There are four font properties you can change.

`\fontencoding`
>The font encoding, such as OT1 (TeX default) or T1 (extended characters support, better PDF support, widely used).

`\fontfamily`
>The font family.

`\fontseries`
>The series: l=light, m=medium, b=bold, bx=very bold.

`\fontshape`
>The shape: it=italic, n=normal, sl=slanted, sc=small capitals.

```latex
{
\fontfamily{anttlc}\selectfont
Some text in anttlc...
}
```

The `\selectfont` command is mandatory, otherwise the font will not be changed. It is highly recommended to enclose the command in a group to cleanly return to the previous font selection when desired.

You can use all these commands in a row:

```latex
{
\fontencoding{T1}\fontfamily{anttlc}\fontseries{m}\fontshape{n}\selectfont
Some text in anttlc...
}
```

For short, you can use the `\usefont{<encoding>}{<family>}{<series>}{<shape>}` command.

It's often useful to wrap this in a macro:

`\newcommand*{\myfont}{\fontfamily{<familyname>}\selectfont}`

If this is something you will be doing a lot, it would make more sense to turn it into a proper environment:

`\newenvironment{myfont}{\fontfamily{<familyname>}\selectfont}{\par}`

Then you use it like any environment:
```
\begin{myfont}
  Some text in the new font.
\end{myfont}
```

You can also define a command corresponding to the standard font changing commands such as \textrm or \textsf, but using your particular font:

`\DeclareTextFontCommand{\textmyfont}{\myfont}`

Use this like the standard commands:

`Text in the default font. \textmyfont{Text in the new font.} Again text in the default font.`

An advantage of this command over the simpler version described above is automatic italic correction, cf. [Why use \DeclareTextFontCommand vs. just \newcommand?](http://tex.stackexchange.com/q/47259).

## Arbitrary font size

You may choose a particular font size with the `\fontsize{<size>}{<line space>}` command. Example:

`{\fontsize{5cm}{1em}\selectfont This is big!}`

## Using arbitrary system fonts

Use in `XeTeX` and `LuaTeX` with package `fontspec`

# Software

## [Pango](http://www.pango.org/)

## [fontconfig](https://www.freedesktop.org/wiki/Software/fontconfig/)

- [Arch Linux - fontconfig](https://wiki.archlinux.org/index.php/Font_configuration)

# Fonts

## Popular fonts

| Sans Serif (paper) | Serif (screen) |
| -                  | -              |
| Times New Roman    | Arial          |
| Georgia            | Helvetica      |
| Bookman Old Style  | Tahoma         |
|                    | Ubuntu         |
|                    | Robotto        |
|                    | Open Sans      |

# Tips and Tricks

## When to use Serif vs. Sans Serif Fonts?

- Serif (Times New Roman)
    + body text to pull the letters together => easier to read on paper
    + pull the reader through the text
- Sans Serif (Arial)
    + good with big title, headings

# References

