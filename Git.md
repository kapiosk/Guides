# Git

## Github

Install

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install git
```

Config

```bash
git config --global user.name "Your name here"
git config --global user.email "your_email@example.com"
```

Create Keys

```bash
ssh-keygen -t rsa -C "your_email@example.com"
```

Copy Public Key

```bash
more ~/.ssh/id_rsa.pub
```

Go to your [SSH keys in Account settings](https://github.com/settings/keys) and add the new key

Check config by using

```bash
ssh -T git@github.com
```

Set origin for local project

```bash
git remote add origin samplepath:sample.git
```

## Advanced

Pushing to multiple Git repos

```bash
# Add Git repo as cake
git remote add cake git@ssh.dev.azure.com:v3/Potato
# Register repo as push url
git remote set-url --add --push cake git@ssh.dev.azure.com:v3/Potato
# Add next git
git remote set-url --add --push cake git@github.com:Potato.git
# Push to both
git push cake
```

Change email

```bash
git config --global user.email {ID}+{username}@users.noreply.github.com
git commit --amend --reset-author
```

__Please note that you cannot pull from multiple repos!!!__

## Windows

Create SSH key for Git from the Git GUI application:

![Image of Git Credentials](/Images/vmplayer_JrbsuuFtAv.png)

Then proceed as normal
