# Configure SSH

Most of our work on libraries systems happens via SSH. 

## Generate an SSH Key pair

We use public/private key pairs to authenticate SSH connections. 

To generate a key pair, start the MSYS2 Shell, and run the following command  
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Fill in your personal email and a strong passphrase, but it's fine to accept the rest of the defaults. If you change the name of the key files, you may need to account for that in the `ssh-agent` script below. 

If you took the defaults, this will create two key files and put them in your home directory at `~/.ssh`: 
* `id_rsa.pub`, which you will share out with various 3rd parties to allow them to verify your identity 
* `id_rsa`, a private key file that you should keep secret and treat like a password. 

To use your new key, create a file at `~/.ssh/config` and add something like the following Host block:

```
Host *
  ForwardAgent yes
  User jdoe
  IdentityFile /home/doe0000/.ssh/id_rsa
```



## Set up SSH Agent

Fetch our ssh-agent.sh script and wire it up to work with your new MSYS2 install with the following multi-line command:
```
curl -OL https://github.com/OULibraries/msys2-setup/raw/master/ssh-agent.sh && \
chmod +x ssh-agent.sh && \
mv ssh-agent.sh /etc/profile.d/
```
This script checks to make sure that the ssh-agent keymanager is running and has access to your keys when you open a new MSYS2 shell. 

## Set up your SSH Key at GitHub

Follow GitHub's [instructions for adding an ssh key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows) to your account, then add the following to your ssh config and and [test your ssh connection](https://help.github.com/articles/testing-your-ssh-connection/) with GitHub.

```
Host github.com
    User git
```

## Send your public key to Ops

You'll need to send your publc key to someone who can add you in to the system. That probably means emailing `id_rsa.pub` to Jason. <b>Do not send your private key!</b>

## Install the OU Libraries standard ssh config

Once you can connect to GitHub, you'll need to get [our OU Libraries ssh config](https://github.com/OULibraries/ssh_config) and configure your ssh keys for use with our systems. This is a private repository, so you may need to request access. 
