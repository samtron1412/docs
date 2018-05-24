[TOC]

# LaTeX

## Packages should load in LaTeX

### [nag](http://www.ctan.org/pkg/nag)

Warns when you accidentally use deprecated LaTeX constructs from
**l2tabu**. Place below line before the `\documentclass`:

`\RequirePackage[l2tabu, orthodox]{nag}`

### [microtype](http://www.ctan.org/pkg/microtype)

It plays with ever-so-slightly shrinking and stretching of the fonts and
with the extent to which text protrudes into the margins in a way that
yields results that look better, that have fewer instances of
hyphenation, and fewer overfull *hboxes*.

`\usepackage[stretch=10]{microtype}`

### [hyperref](http://tug.org/applications/hyperref/)

Extensive support for hypertext in LATEX.

### [geometry](http://www.ctan.org/pkg/geometry)

Flexible and complete interface to document dimensions.

### [AMS math packages](http://ctan.org/pkg/amsmath)
### [urlbst](http://nxg.me.uk/dist/urlbst/)

Web support for BibTEX.

### [booktabs](http://www.ctan.org/pkg/booktabs)

Publication quality tables in LATEX.

### [array](http://www.ctan.org/pkg/array)

Extending the array and tabular environments.

### [memoir](http://www.ctan.org/pkg/memoir)

Typeset fiction, non-fiction and mathematical books

### [koma-script](http://www.ctan.org/pkg/koma-script)

A bundle of versatile classes and packages.


### [TikZ](http://sourceforge.net/projects/pgf/)

TikZ and PGF are TeX packages for creating graphics programmatically.
TikZ is build on top of PGF and allows you to create sophisticated
graphics in a rather intuitive and easy manner.

### [graphicx]()

### enumerate

enumerated environment

### fancyhdr

Create header

### longtable

### [listing](http://www.ctan.org/tex-archive/macros/latex/contrib/listings/)

### [verbatim]()

## Bibliography

### Back-end bibliography processor

#### [BibTeX](https://en.wikipedia.org/wiki/BibTeX)

BibTeX is reference management software for formatting lists of
references. BibTeX was created by Oren Patashnik and Leslie Lamport in
1985. It is written in WEB/Pascal.

##### Basic structure

Input:

- An `.aux` file produced by LaTeX on an earlier run.
- A `.bst` file (the style file), which specifies the general reference-list style and specifies how to format individual entries, and which is written by a style designer [..] in a special-purpose language [..].
- A `.bib` file(s) create a database of all reference-list entries the user might ever hope to use.

BibTeX chooses from the `.bib` file(s) only those entries specified by the `.aux` file (that is, those given by LaTeX's `\cite` or `\nocite` commands), and creates as **output** a `.bbl` file containing these entries together with the formatting commands specified by the `.bst` file [..]. LaTeX will use the `.bbl` file, perhaps edited by the user, to produce the reference list.

`aux + bib -> bbl + bib -> ref list`

##### [Style examples](http://www.cs.stir.ac.uk/~kjt/software/latex/showbst.html)

##### [bib file](https://en.wikipedia.org/wiki/BibTeX#Bibliographic_information_file)

- Cross-referencing.
- Using more than one bib file.
- Non-reference section
	+ @COMMENT{...}


#### [Biber](http://biblatex-biber.sourceforge.net/)

[manual](http://mirrors.ctan.org/biblio/biber/documentation/biber.pdf)

### Packages
- `\cite{cite_key}`
- `\cite[p.~215]{citation01}`
- `\cite{citation01,citation02,citation03}`
- `\nocite{citation01}` : ref appear in bibliography but not where it is ref in the main text.

#### [natbib](http://ctan.org/pkg/natbib)
[ref sheet](http://merkel.zoneo.net/Latex/natbib.php)

- `\usepackage[options]{natbib}`
		<figure>
		  <figcaption style="text-align:center;">Natbib Options</figcaption>
		  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
		  <img src="latexFigures/natbiboptions.png" alt="Natbib Options" title="Natbib Options">
		</figure>
- `\bibliographystyle{plainnat}`
		<figure>
		  <figcaption style="text-align:center;">Styles compatible with Natbib</figcaption>
		  <hr style="width:70%;margin-left:auto;margin-right:auto;" />
		  <img src="latexFigures/stylesnatbib.png" alt="Styles compatible with Natbib" title="Styles compatible with Natbib">
		</figure>

#### [biblatex](http://www.ctan.org/pkg/biblatex)


# Tutorial

## [Popular packages in latex](https://tex.stackexchange.com/questions/553/what-packages-do-people-load-by-default-in-latex)


## [Problems with Vietnamese](http://vntex.sourceforge.net/vntexse4.html)

## Set up for includegraphic

- Use variable environment **TEXINPUTS** to set up path to directory
  contain figures. Eg. **TEXINPUTS=E:/Software/Report/Figures**
- Use package graphicx to include figures.

## [Integrating Local Additions](http://docs.miktex.org/manual/localadditions.html)

Use to install offline, manual package at local.

## Miktex packages

Use package manager to install packages, change repositories to have
best speed.

## Bibliography

Use biber package

# Tips and Tricks

## [Latex templates](https://github.com/bamos/latex-templates)


# Alternatives

- https://tex.stackexchange.com/questions/120271/alternatives-to-latex

# References
