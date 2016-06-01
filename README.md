# OU Libraries Standard MSYS2 Developer Setup

This guide covers the installation of a basic CLI toolset for Windows users. 

## Install MSYS2 64
Get msys2  from http://msys2.github.io/

You want the x86_64 version. Following the instructions at the
download site and accepting the installer defaults should result in a
generally worky MSYS2 intall. Make sure to run command line steps for
updating the package database and pacman.

If you have any problems, refer to the [full installation
instructions](https://sourceforge.net/p/msys2/wiki/MSYS2%20installation)
or grab a team member.



### Unify MSYS2 and Windows homes

We like to have our user folders unified between MSYS2 and Windows. 

First, open the windows command prompt (cmd) as administrator. Then
Copy the default configuration files from your MSYS2 home to your
Windows home.

```
copy C:\msys64\home\%USERNAME%\* %USERPROFILE%
```

In the same command prompt window, backup your original msys2 home
folder, just in case.

```
rename C:\msys64\home\%USERNAME% %USERNAME%.bak
```

Then, (still in the same window) create a link so that your Windows
home directory will be used as your MSYS2 home directory

```
mklink /D C:\msys64\home\%USERNAME% %USERPROFILE%
```

### Set up MSYS2 to run as Admin
Life is easier in Vagrant if we alwasy just run msys2 as Admin.  To do so:

* Search for "msys2" in and right click the app
* Click "Open file Location"
* Right click "MSYS2 Shell"
* Click properties
* Click advanced
* Check "Run as administrator"
* Click OK
* Click OK
* Close out the file explorer



### Install some basic tools

`pacman` is the MSYS2 package manager, and can be used to search for and install lots of packages. 

Running the following will give you python2, git, and a couple of editors. 

```
pacman -S --needed --noconfirm \
mingw64/mingw-w64-x86_64-python2 \
mingw64/mingw-w64-x86_64-emacs \
msys/vim \
msys/nano \
msys/git \
```

See the [full docs for pacman](https://wiki.archlinux.org/index.php/pacman) if you want to learn more. 



## Configure Vim

Create a ~/.vimrc file that keeps vim from falling back on strict vi emulation: 

```
echo "set nocompatible" >> ~/.vimrc
```

## Configure SSH

### Generate an SSH Key

In the msys2 shell, run  
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
to generate an ssh keys. Fill in your personal email and a strong passphrase, but accept the defaults for everything else, including the key name and location.

### Set up SSH Agent

Fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/msys2-setup/raw/master/ssh-agent.sh && \
chmod +x ssh-agent.sh && \
mv ssh-agent.sh /etc/profile.d/ && \
mkdir .ssh && \
chown 700 .ssh
```
Then close and reopen msys2

### Set up your SSH Key at GitHub

Follow GitHub's [instructions for adding an ssh key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows) to your account, and [testing your ssh connection](https://help.github.com/articles/testing-your-ssh-connection/) with GitHub. 
