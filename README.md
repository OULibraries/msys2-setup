get msys2 x64
http://msys2.github.io/

Open CMD as administrator, run the following:
```
copy C:\msys64\home\%USERNAME%\* %USERPROFILE%
del /Q C:\msys64\home\%USERNAME%
mklink /D C:\msys64\home\%USERNAME% %USERPROFILE%
```

Search msys2 in start and right click the app
Click "Open file Location"
right click "MSYS2 Shell"
click properties
Click advanced
Check "Run as administrator"
Click OK
Click OK

run msys2

Run
```
update-core
```
close and reopen msys2

Run
```
pacman -Su --noconfirm
```
Run
```
pacman -S --needed --noconfirm \
mingw64/mingw-w64-x86_64-python2 \
mingw64/mingw-w64-x86_64-emacs \
msys/git msys/nano
```
Then
```
curl -OL https://github.com/OULibraries/MinGW-Setup/raw/master/msys/1.0/etc/profile.d/ssh-agent.sh
chmod +x ssh-agent.sh
mv ssh-agent /etc/profile.d/
mkdir .ssh
chown 700 .ssh
```

close and reopen msys2
