## Install MSYS2 64
Get msys2  from http://msys2.github.io/


##  Unify MSYS2 and Windows homes
We like to have our user folders unified between msys2 and windows.

Open CMD as administrator, run the following:
```
copy C:\msys64\home\%USERNAME%\* %USERPROFILE%
rmdir /Q C:\msys64\home\%USERNAME%
mklink /D C:\msys64\home\%USERNAME% %USERPROFILE%
```

## Set up MSYS2 to run as Admin
Life is easier in Vagrant if we just run msys2 as Admin.  To do so:

* Search msys2 in start and right click the app
* Click "Open file Location"
* Right click "MSYS2 Shell"
* Click properties
* Click advanced
* Check "Run as administrator"
* Click OK
* Click OK
* Close out the file explorer

## Update MSYS2 and install some packages

Run msys2 from the start menu

Update msys2 core by running
```
update-core
```
close and reopen msys2

Update msys2 packages by running
```
pacman -Su --noconfirm
```
Install our various utilities and helpers
```
pacman -S --needed --noconfirm \
mingw64/mingw-w64-x86_64-python2 \
mingw64/mingw-w64-x86_64-emacs \
msys/vim \
msys/nano \
msys/git 
```

# Configure Vim

Too keep vim from falling back on strict vi emulation, create a ~/.vimrc file and add the following line:

```
set nocompatible
```




# Set upSSH Agent

Fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/MinGW-Setup/raw/master/msys/1.0/etc/profile.d/ssh-agent.sh
chmod +x ssh-agent.sh
mv ssh-agent.sh /etc/profile.d/
mkdir .ssh
chown 700 .ssh
```

Then close and reopen msys2
