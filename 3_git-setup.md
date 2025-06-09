---
title: "Setup Git Configs"
teaching: 10
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- set up basic configs for Git

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How do I first set up Git?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Setting up Git

When we use Git on a new computer for the first time,
we need to configure a few things. Some basic configurations to set for Git are:

- your name 
- your email address,
- your preferred text editor

To start we will check in on our current Git configuration. Open your shell terminal window and type:

```bash
$ git config --list
```

:::::::::::::::::::: instructor
On MacOS, without any configuration your output might look like this:

```output
credential.helper=osxkeychain
```

On Windows, without any configuration your output might look like this:

```output
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=openssl
http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
core.autocrlf=true
core.fscache=true
core.symlinks=false
pull.rebase=false
credential.helper=manager-core
credential.https://dev.azure.com.usehttppath=true
init.defaultbranch=main
```

If you have different output, then you may have your Git configured already. If you have not configured Git, we will do that together now.

:::::::::::::::::::::::::::::

First, we will tell Git our user name and email.

Please note: You need to use the same email address in your Git configuration in the shell as you entered into GitHub when you created your GitHub account. Later in the lesson we will be using GitHub and the email addresses need to match. If you are concerned about privacy, please review [GitHub's instructions for keeping your email address private](https://help.github.com/articles/keeping-your-email-address-private/).

Type these two commands into your shell, using your own name and email:

```bash
$ git config --global user.name "Loki Odinson"
$ git config --global user.email "loki.odinson@tva.org"
```

If you enter the commands correctly, the shell will merely return a command prompt and no messages. To check your work, ask Git what your configuration is using the same command as above:

Let's also set our default text editor. A text editor is necessary with some of your Git work, and the default from Git is Vim, which is a text editor that is hard to learn at first. Since we are using VS Code for this lesson, we will set the default editor to `code`. You can feel free to change this at a later time.

```bash
$ git config --global core.editor "code --wait"
```

```bash
git config --list
```

```output
user.name=Loki Odinson
user.email=loki.odinson@tva.org
core.editor=code --wait
```

:::::::::::::::::::::::: callout

## Line Endings

As with other keys, when you hit the 'return' key on your keyboard, 
your computer encodes this input. 
For reasons that are long to explain, different operating systems
use different character(s) to represent the end of a line. 
(You may also hear these referred to as newlines or line breaks.)
Because git uses these characters to compare files, 
it may cause unexpected issues when editing a file on different machines. 

You can change the way git recognizes and encodes line endings
using the `core.autocrlf` command to `git config`.
The following settings are recommended:

On OS X and Linux:

```bash
$ git config --global core.autocrlf input
```

And on Windows:

```bash
$ git config --global core.autocrlf true
```

You can read more about this issue 
[on this GitHub page](https://help.github.com/articles/dealing-with-line-endings/).

::::::::::::::::::::::::::::::

:::::::::::::::::::::::: callout

## Default Git branch naming

```bash
$ git config --global init.defaultBranch main
```

Source file changes are associated with a "branch." 
By default, Git will create a branch called `master` 
when you create a new repository with `git init`. This term evokes 
the racist practice of human slavery and the 
[software development community](https://github.com/github/renaming)  has moved to adopt 
more inclusive language. 

In 2020, most Git code hosting services transitioned to using `main` as the default 
branch. As an example, any new repository that is opened in GitHub and GitLab default 
to `main`.  However, Git has not yet made the same change.  As a result, local repositories 
must be manually configured have the same main branch name as most cloud services.  

For versions of Git prior to 2.28, the change can be made on an individual repository level. Note that if this value is unset in your local Git 
configuration, the `init.defaultBranch` value defaults to `master`.

Since we are creating the repository on GitHub, the default branch name for the `multiverse` repo will be `main`. Configure this setting if you plan on creating git repositories locally first.

::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Version control helps track changes to files and projects
- Git and GitHub are not the same
- Git commands are written as `git verb options`
- When we use Git on a new computer for the first time, we need to configure a few things

::::::::::::::::::::::::::::::::::::::::::::::::::


