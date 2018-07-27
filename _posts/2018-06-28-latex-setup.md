---
layout: post
title: My LaTeX Setup
author: Diana Cai
tags:
- other
- productivity
- tools
- misc
summary: I'll describe my current LaTeX setup: vim, skim, and latexmk. I currently write notes and papers using LaTeX on a Mac, though in a previous life, my setup on Linux was very similar
---

I'll describe my current LaTeX setup: vim, skim, and latexmk.
I currently write notes and papers using LaTeX on a Mac, though in a previous life, my setup on Linux was very similar (i.e., ```s/macvim/gvim/g``` and ```s/skim/zathura/g```).
I like being able to use my own customized text editor (with my favorite keyboard shortcuts) to edit a raw text file that I can then put under version control.
Though I describe things with respect to vim, most of this setup can also
achieved with some other text editor, e.g., emacs or sublime.

## The basic setup

### Text editor: vim

I use the text editor, [vim](https://vim.rtorr.com/). For writing documents, I often also like using [macvim](http://macvim-dev.github.io/macvim/), which is
basically vim but with a few extra GUI features, such as scrolling and text
selection features.

### PDF reader: Skim

For my pdf reader, I use the [Skim app](https://skim-app.sourceforge.io/). The nice thing about Skim is that it will
autoupdate the pdf after you compile the tex and keep the document in the same
place. By contrast, Preview will refresh the document and reload it from the
beginning of the document, which is quite cumbersome if you'd just edited text on page 5.

### Compilation: latexmk + vim keybindings

In vim, I have several keybindings set up in my .vimrc file.
Currently, I compile the .tex file using [latexmk](http://mg.readthedocs.io/latexmk.html).
Files can be compiled to pdf with the command

```bash
latexmk -pdf [file]
```

In latexmk, you can also automatically recompile the tex when needed, but I prefer to manually compile the tex.

I have the following key bindings in vim:

* ```control-T``` compiles the tex to pdf using latexmk
* ```shift-T``` opens the pdf in Skim
* ```shift-C``` cleans the directory

For instance, the compile keybinding above is done by adding the following line
to the .vimrc file

```vim
autocmd FileType tex nmap <buffer> <C-T> :!latexmk -pdf %<CR>
```

These types of key bindings can usually be setup with other text editors as well.


### Putting it all together

When I'm writing a document, I'll often have my text editor full screen on the
left and the Skim on the right with the pdf open. After making edits, I'll press
```control-T``` to compile and the pdf will auto-refresh in Skim.

<div align="center">
<img src="{{site.baseurl}}/assets/latex-setup.png" align="center" width="700"
alt="LaTeX Skim Vim Setup">
<p>Example of macvim next to Skim setup. Monitor recommended :)</p>
<br />
</div>

## Tools for writing LaTeX documents

There are a few other tools that I use for writing papers (or extensive notes on
work) that I'll list below that save me a lot of time.

### Plugins: snippets

In vim, I have several [plugins](https://github.com/VundleVim/Vundle.vim) I have in my .vimrc file. For writing papers, I
use ()[snippets] extensively. My most used command is typing ```begin <tab>```, which
allows me to allows me to autocomplete the parts of LaTeX that I don't want to
spend time typing but use often. For instance, in the TeX below, snippets means
I only have to type ```align*``` once.

```tex
\begin{align*}
    \pi(\theta | x) = \frac{\pi(\theta) p(x | \theta)}
                           {\int \pi(\theta) p(x | \theta) d\theta}
\end{align*}
```

And should I need to change ```align*``` to just ```align```, I only have to
edit this in one of the parens instead of in both lines.

To use [vim plugins](https://github.com/VundleVim/Vundle.vim) (after installing), you just need to add the github page to your .vimrc file, e.g., for
[Ultisnips](https://github.com/SirVer/ultisnips), add the line

```vim
Plugin 'SirVer/ultisnips'
```

and execute ```:PluginInstall``` while in command mode in vim.

### TeX skeleton
For writing quick notes, I have a TeX skeleton file that always loads when I
start a new vim document, i.e., when executing ```vim notes.tex``` in the
command line, a fully-functional tex skeleton with all the packages I normally use and font styles are
automatically loaded. E.g., a version of the following:

```tex
\documentclass[11pt]{article}

\usepackage{amsmath, amssymb, amsthm, bbm}
\usepackage{booktabs, fancyhdr, verbatim, graphicx}

\title{title}
\author{Diana Cai}

\begin{document}

\maketitle

\end{document}

```

### subfiles

For longer documents, I use the [subfiles package](https://en.wikibooks.org/wiki/LaTeX/Modular_Documents#Subfiles) extensively.
This allows me to split a document into smaller files, which can then be
individually compiled into its own document. Subfiles inherit the packages, etc.,
that are defined in the main file in which the subfiles are inserted.

The advantage of using subfiles is that you
can just edit the subfile you're currently focusing on, which is much faster
than compiling the entire document (especially one with many images and references).
This also helps with reducing the number of git conflicts one encounters when
collaborating on a document.

### macros

I have a set of macros that I commonly use that are imported when I load a .tex
document. For writing papers, I'll include a separate macros.tex file with all
of my macro definitions that I reuse often. Some example macros I've defined:

* ```\reals``` for ```\mathbb{R}```
* ```\E``` for ```\mathbb{E}```
* ```\iid``` for ```\stackrel{\mathrm{iid}}{\sim}```
* ```\convas``` for ```\stackrel{\mathrm{a.s.}}{\longrightarrow}```

Also super convenient if you're defining a variable that is always bold if, for
instance, that variable is a vector.


### commenting

My collaborators and I often have a commenting file we use to add various comments (in different colors too!) in the margins, in the text, or highlighting certain regions of the text.
An alternative is to use a [LaTeX commenting package](https://ctan.org/pkg/todonotes)
and then define custom commands controlling how the comments appear in the text.


## .vimrc

You can check out my .vimrc file on [github](https://github.com/dicai/dotfiles/blob/master/vimrc) to see how I set up keybindings, plugins, and
my .tex skeleton file.
