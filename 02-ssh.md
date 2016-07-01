# Configure SSH

Most of our work on libraries systems happens via SSH. 

## Generate an SSH Key pair

We use public/private key pairs to authenticate SSH connections. 

To generate a key pair, start the MSYS2 Shell, and run the following command  
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Fill in your personal email and a strong passphrase, but it's fine to accept the rest of the defaults. If you change the name of the key files, you may need to account for that in the `ssh-agent` script below. 

## Set up SSH Agent

Fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/msys2-setup/raw/master/ssh-agent.sh && \
chmod +x ssh-agent.sh && \
mv ssh-agent.sh /etc/profile.d/ && \
mkdir .ssh && \
chown 700 .ssh
```
Then close and reopen msys2

## Set up your SSH Key at GitHub

Follow GitHub's [instructions for adding an ssh key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows) to your account, and [testing your ssh connection](https://help.github.com/articles/testing-your-ssh-connection/) with GitHub.


## Install the OU Libraries standard ssh config

Once you can connect to GitHub, you'll need to get [our standard ssh config](https://github.com/OULibraries/ssh_config) and configure your ssh keys for use with our systems. This is a private repository, so you may need to request access. 
