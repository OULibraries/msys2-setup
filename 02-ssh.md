# Configure SSH

Most of our work on libraries systems happens via SSH. 

## Generate an SSH Key pair

We use public/private key pairs to authenticate SSH connections. 

To generate a key pair, start the MSYS2 Shell, and run the following command  
```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Fill in your personal email and a strong passphrase, but it's fine to accept the rest of the defaults. If you change the name of the key files, you may need to account for that in the `ssh-agent` script below. 

This will create two key files. A `.pub` file, which you will share out with various 3rd parties to allow them to verify your identity, and a private key file that you should keep secret and treat like a password. 

Set this key up for use by adding something like the following to `~/.ssh/config`

```
Host *
  ForwardAgent yes
  User jdoe
  IdentityFile /home/doe0000/.ssh/id_rsa
```


## Set up SSH Agent

Fetch some of the config we figured out in the MinGW days
```
curl -OL https://github.com/OULibraries/msys2-setup/raw/master/ssh-agent.sh && \
chmod +x ssh-agent.sh && \
mv ssh-agent.sh /etc/profile.d/ && \
mkdir -p .ssh && \
chmod 700 .ssh && \
touch .ssh/config
```

## Set up your SSH Key at GitHub

Follow GitHub's [instructions for adding an ssh key](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/#platform-windows) to your account, then add the following to your ssh config and and [test your ssh connection](https://help.github.com/articles/testing-your-ssh-connection/) with GitHub.

```
Host github.com
    User git
```

## Send your public key to Ops

You'll need to send your publc key to someone who can add you in to the system. That probably means emailing `id_rsa.pub` to Jason. 

## Install the OU Libraries standard ssh config

Once you can connect to GitHub, you'll need to get [our standard ssh config](https://github.com/OULibraries/ssh_config) and configure your ssh keys for use with our systems. This is a private repository, so you may need to request access. 
