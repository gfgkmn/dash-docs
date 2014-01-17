# Helm Dash

## What's it

This package uses [Dash](http://www.kapeli.com/dash) docsets inside
emacs to browse documentation. Here's an
[article](http://puntoblogspot.blogspot.com.es/2014/01/ann-helm-dash-documentation-browser-for.html)
explaining the basic usage of it.

![](https://raw.github.com/areina/helm-dash/master/misc/helm-dash.gif)

## What's not

If you're looking for dash.el, the list library, please go to
[dash.el](http://www.github.com/magnars/dash.el)


## Requirements

- [helm](https://github.com/emacs-helm/helm)
- [esqlite](https://github.com/mhayashi1120/Emacs-esqlite)

Previously, we were using [sqlite](https://github.com/cnngimenez/sqlite.el)
but we had some problems with it because it was returning different
results for the same sql query.

## Installation

It's available on [MELPA](http://melpa.milkbox.net).

`m-x package-install helm-dash RET`

## Usage

`m-x helm-dash RET` will run helm with your active docsets
loaded. Typing substrings of what you search will find-as-you-type.

- The search starts from 3 chars.
- Install new docsets with m-x helm-dash-install-docset
- After installing a new docset, add the name of the docset to
  `helm-dash-common-docsets' or in 'helm-dash-docsets' (which is ment
  to be buffer local)

`m-x helm-dash-at-point RET` is like helm-dash, but it will prefill
the search input with the symbol at point.

The command `helm-dash-reset-connections` will clear the connections
to all sqlite db's. Use it in case of errors when adding new docsets.
The next call to `helm-dash` will recreate them.

## Sets of Docsets

### Common docsets

`helm-dash-common-docsets' is a list that should contain the docsets
to be active always. In all buffers.

### Buffer local docsets

Different subsets of docsets can be activated depending on the
buffer. For the moment (it may change in the future) we decided it's a
plain local variable you should setup for every different
filetype. This way you can also do fancier things like project-wise
docsets sets.

``` elisp
(defun go-doc ()
  (interactive)
  (setq-local helm-dash-docsets '("Go")))

(add-hook 'go-mode-hook 'go-doc)
```

## Caveats

helm-dash has been tested only in linux.  We've been notified that it doesn't work in Mac, so we ask for elisp hackers who own something that runs Mac OSX if they could take a look at it. 

Hints: It looks like something with 'end of line' differences. The suspicious are [esqlite](http://www.github.com/mahayashi1120/Emacs-sqlite) (which helm-dash requires) or [pcsv](http://www.github.com/mahayashi1120/Emacs-pcsv) (which esqlite requires)

## Authors

- Toni Reina <areina0@gmail.com>
- Raimon Grau <raimonster@gmail.com>
