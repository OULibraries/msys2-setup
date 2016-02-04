get msys2 x64
http://msys2.github.io/

We like to have our user folders unified between msys2 and windows.

Open CMD as administrator, run the following:
```
copy C:\msys64\home\%USERNAME%\* %USERPROFILE%
rmdir /Q C:\msys64\home\%USERNAME%
mklink /D C:\msys64\home\%USERNAME% %USERPROFILE%
```

Life is easier in Vagrant if we just run msys2 as Admin.  To do so:

Search msys2 in start and right click the app
Click "Open file Location"
right click "MSYS2 Shell"
click properties
Click advanced
Check "Run as administrator"
Click OK
Click OK
Close out the file explorer

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
Then, fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/MinGW-Setup/raw/master/msys/1.0/etc/profile.d/ssh-agent.sh
chmod +x ssh-agent.sh
mv ssh-agent.sh /etc/profile.d/
mkdir .ssh
chown 700 .ssh
```

close and reopen msys2
