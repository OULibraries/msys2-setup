# Helpful(?) Extras for Windows Devs

The following hints and tools are things that some devs have found to be
helpful when working on Windows. 


## Map Caps Lock to Control

[Ctrl2Cap](https://technet.microsoft.com/en-us/sysinternals/bb897578.aspx) is a
tool for turning your caps lock key in to a second control key that has worked
reliably across several versions of Windows. 


## Package Management

The [Chocolatey](https://chocolatey.org/) package manager can install thousands
of Windows tools including things like Notepad++, Firefox, Vagrant, and more. 

Many CLI packages for things like `rsync` and `curl` are also available, but
we've mostly standardized on the MSYS2 provided version of those tools, and
mixing other versions in could lead to unpredictable results.    

## Piping to/from the Clipboard

The [pasteboard](https://chocolatey.org/packages/pasteboard) package from
Chocolatey installs a Windows port of the MacOS `pbcopy` and `pbpaste`
utilities. Alternately, the Windows built in `clip` can be used in place of
`pbcopy`.


## Starter Config Files for CLI tools 

Many command line tools have lots of configuration options. These are
reasonable starter configs for people interested in customizing their
environments.

* [Sensible Bash](https://github.com/mrzool/bash-sensible)
* [Sensible.vim](https://github.com/tpope/vim-sensible)


## Quick Local Drupal Sandbox

Serious Drupal dev work should happen in our vagrant-based environments to
ensure compatibility with production, but [Acquia Dev
Desktop](https://www.acquia.com/downloads) is ideal for doing quick experiments
and learning more about Drupal. 


## Text Editors

Some good text editors, if you don't already have a favorite

* [Notepad++](https://notepad-plus-plus.org/)
* [Atom](https://atom.io/)


