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

Create a ~/.vimrc file that keeps vim from falling back on strict vi emulation: 

```
echo "set nocompatible" >> ~/.vimrc
```

# Set up SSH Agent

Fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/msys2-setup/raw/master/ssh-agent.sh
chmod +x ssh-agent.sh
mv ssh-agent.sh /etc/profile.d/
mkdir .ssh
chown 700 .ssh
```
Then close and reopen msys2


# Generate an SSH Key and let ssh-agent know about it

In the msys2 shell, run  
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
to generate an ssh keys. Fill in your personal email, but accepting the details for everything else is OK.

Then run 

```
ssh-add ~/.ssh/id_rsa
``` 
to let ssh-agent know about the newly created ssh key. 


# Set up your SSH Key at GitHub

Follow GitHub's [instructions for adding an ssh key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows) to your account, and [testing your ssh connection](https://help.github.com/articles/testing-your-ssh-connection/) with GitHub. 
