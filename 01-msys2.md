# Install MSYS2 64

Get MSYS2  from http://msys2.github.io/

You almost certainly want the x86_64 installer. Following the
instructions at the download site, and using the installer defaults
should result in a generally worky MSYS2 intall. Make sure to run the
command line steps for updating the package database and pacman.

If you have any problems, refer to the [full installation
instructions](https://sourceforge.net/p/msys2/wiki/MSYS2%20installation)
or grab a team member.

## Unify MSYS2 and Windows homes

We like to link have a single directory serve as both our MSYS2 home 
directory  (`/home/doe0000`) and our Windows home directory (`C:\Users\doe0000`). 
In order to do that, we'll make the MSYS2 path a link to the Windows one. 

First, open a Windows command prompt (cmd) as Administrator. Then
run the following copy command to duplicate the default configuration 
files from your MSYS2 home to your Windows home.

```
copy C:\msys64\home\%USERNAME%\* %USERPROFILE%
```

In the same cmd window, move your original msys2 home
folder out of the way, just in case.


```
rename C:\msys64\home\%USERNAME% %USERNAME%.bak
```

Then, (still in the same window) create a link so that your Windows
home directory will be used as your MSYS2 home directory. This is the 
only step that really needs Administrator privleges. 

```
mklink /D C:\msys64\home\%USERNAME% %USERPROFILE%
```

## Install Some Tools

`pacman` is the MSYS2 package manager, and can be used to search for and install lots of packages. 

Running the following will give you python2, git, and a couple of editors. 

```
pacman -S --needed --noconfirm \
mingw64/mingw-w64-x86_64-python2 \
msys/vim \
msys/nano \
msys/git \
msys/rsync \
msys/tar \
msys/gzip 
```

See the [full docs for pacman](https://wiki.archlinux.org/index.php/pacman) if you want to learn more.  Many other packages are available. 


## Configure Vim

Create a `~/.vimrc` file that turns on syntax highlighting and keeps vim from falling back on strict vi emulation: 

```
echo "set nocompatible" >> ~/.vimrc
echo "syntax on" >> ~/.vimrc
```

If you become a habitual vim user, you may wish to look at other vim configuration options and add-ons. The [sensible.vim](https://github.com/tpope/vim-sensible) project is a good place to get started.



## Set up Git

The following git settings should be configured in the MSYS setup and, later,  on other environments where you'll be running git. 

Configure your identity
```
git config --global user.email "jdoe@example.com"
git config --global user.name "Jane Doe"
```

Set up colorized git output. 
```
git config --global color.ui true
```

Set up new push behavior, rather than old default. 
```
git config --global push.default simple
```


