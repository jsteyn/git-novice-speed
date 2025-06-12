---
title: "Setup Instructions"
teaching: 0
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What software do I need to have installed?
- Do I have a GitHub account?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Install VS Code and other needed software
- Connect VS Code to GitHub

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

If you are participating in this workshop remotely (e.g. over Zoom), it is highly recommended that you use two screens: 1 screen with the remote meeting, to see the instructor sharing their screen, and 1 screen with your applications. You will need to have an editor (such as Notepad++) and a web browser open to GitHub.com in order to follow along. Notepad++ is a free and open source editor. On Mac and Linux there are usually various editors available by default.

![Notepad++ Screenshot](https://notepad-plus-plus.org/assets/images/notepad4ever.png))

:::::::::::::::::::::::::::::::::::::

## Create a GitHub account

If you do not already have a GitHub account, visit [github.com](https://github.com) to create one.

You can refer to [this doc page](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github) for further instructions about creating a GitHub account.

If you already have a GitHub account, please verify that you can sign in, and take note of the email(s) associated with the account.

It is strongly recommended that you set up 2FA for your GitHub account, and to use a password manager.

## Software Installations

### Git

You must have Git installed on your local computer. Typically, Mac and Linux computers come pre-installed with git, while Windows users must install [GitBash](https://gitforwindows.org) (Git for Windows). However, you should verify that Git is installed on your computer.

You can verify git is installed by opening a command line application (e.g. Terminal) and typing: 

```bash
$ git version
```

If you see an error message stating git is an unknown command, you will need to install git.

If you do not already have git installed, you can refer to [this GitHub guide](https://github.com/git-guides/install-git) on installing git for any OS. 

### Bash

You should have a Bash terminal. If you are on a Windows, you will have a Bash terminal by virtue of installing Git for Windows (GitBash). If you are on a Mac or Linux, you will already have a Bash terminal. If you prefer, you can use a similar terminal like Zsh.

Rather than using a seperate command line application, you will be using the Terminal in VS Code. To learn more about using the Terminal in VS Code, refer to [these docs](https://code.visualstudio.com/docs/terminal/basics).

### Create an SSH keypair

To link our local git repository to our GitHub account we will need to generate an ssh keypair. We do this in the bash terminal. At the command prompt, enter the following command:

```bash
$ ssh-keygen -t ed25519 -C "youremail@yourinstitution.ext"
```
```output
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/users/yourname/.ssh/id_ed25519):
```

We want to use the default file, so just pres <kbd>Enter</kbd>.

```output
Created directory `/c/users/yourname/.ssh`.
Enter passphrase (empty for no passphrase):
```
For now we will not using a passphrase, because you will have to enter it every time you push to git. Just press <kbd>Enter<kbd> for no passphrase).

fter entering the same passphrase a second time, we receive the confirmation

```output
Your identification has been saved in /c/users/yourname/.ssh/id_ed25519
Your public key has been saved in /c/users/yourname/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:SMSPIStNyA00KPxuYu94KpZgRAYjgt9g4BA4kFy3g1o youremail@yourinstitution.ext
The key's randomart image is:
+--[ED25519 256]--+
|^B== o.          |
|%*=.*.+          |
|+=.E =.+         |
| .=.+.o..        |
|....  . S        |
|.+ o             |
|+ =              |
|.o.o             |
|oo+.             |
+----[SHA256]-----+
```

The "identification" is actually the private key. You should never share it.  The public key is appropriately named.  The "key fingerprint"
is a shorter version of a public key.

Now that we have generated the SSH keys, we will find the SSH files when we check.

```bash
ls -al ~/.ssh
```

```output
drwxr-xr-x 1 Alfredo   197121   0 Jul 16 14:48 ./
drwxr-xr-x 1 Alfredo   197121   0 Jul 16 14:48 ../
-rw-r--r-- 1 Alfredo   197121 419 Jul 16 14:48 id_ed25519
-rw-r--r-- 1 Alfredo   197121 106 Jul 16 14:48 id_ed25519.pub
```

First, we need to copy the public key.  Be sure to include the `.pub` at the end, otherwise you're looking at the private key.

```bash
cat ~/.ssh/id_ed25519.pub
```

```output
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIDmRA3d51X0uu9wXek559gfn6UFNF69yZjChyBIU2qKI a.linguini@ratatouille.fr
```

Now, going to GitHub.com, click on your profile icon in the top right corner to get the drop-down menu.  Click "Settings", then on the
settings page, click "SSH and GPG keys", on the left side "Access" menu. Click the "New SSH key" button on the right side. Now,
you can add the title, paste your SSH key into the field, and click the "Add SSH key" to complete the setup.

Now that we've set that up, let's check our authentication again from the command line.

```bash
$ ssh -T git@github.com
```

```output
Hi YourName! You've successfully authenticated, but GitHub does not provide shell access.
```

Good! This output confirms that the SSH key works as intended.

:::::::::::::::::::::::::::::::::::::::: keypoints

- GitHub, bash, git and ssh key pairs are needed for this lesson

::::::::::::::::::::::::::::::::::::::::::::::::::
