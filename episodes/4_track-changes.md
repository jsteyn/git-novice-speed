---
title: "Tracking Changes"
teaching: 20
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- How do I record changes in Git?
- How do I check the status of my version control repository?
- How do I record notes about what changes I made and why?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Go through the modify-add-commit cycle for one or more files.
- Explain where information is stored at each stage of that cycle.
- Distinguish between descriptive and non-descriptive commit messages.

::::::::::::::::::::::::::::::::::::::::::::::::

## Loki writes a story about Thor in New Asgard

Loki, in his role as God of Stories, oversees the many branching timelines in the multiverse. But even an infinitely clever being like Loki has trouble keeping track of all of the events across the multiverse. Fortunately, there is a tool that can help keep track of these events across different timeline branches: git! Loki has decided to start logging events in a git repository named `multiverse`. Each planet will have their own file. Loki starts recording the events of New Asgard on Earth, where his brother Thor lives.

## Create a file

First let's make sure we're in the right directory.
You should be in the `multiverse` directory.

```bash
$ pwd
```

Let's create a file called `earth.txt` to start recording the events taking place on the planet Earth.

Open Notepad++. Click on `File` in the menu at the top of the Notepad++ window. Select `Open Folder as Workspace`. Find the directory that you cloned the multiverse repository to and click `Open`

By default an empty new file is created called `new 1`. Type the text below into the editor:



```output
Thor defends New Asgard from invaders.

```

Make sure to end the file with a newline!

Save the file as `earth.txt` by clicking on `File` in the top menu and then `Save as. Navigate to the `multiverse` directory that we cloned our repository to and enter `earth.txt` in the `File name` text box. Press `Save`.

## Track Changes to the File

You can switch between the bash terminal and Notepad using <kbd>Alt-Tab</kbd>. If we check the status of our project again, Git tells us that it's noticed the new file:

```bash
$ git status
```

```output
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        earth.txt

nothing added to commit but untracked files present (use "git add" to track)
```

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.
We can tell Git to track a file using `git add`:

```bash
$ git add earth.txt
```

and then check that the right thing happened:

```bash
$ git status
```

```output
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   earth.txt
```

Git now knows that it's supposed to keep track of `earth.txt`,
but it hasn't recorded these changes as a commit yet.
To get it to do that,
we need to run one more command:

```bash
$ git commit -m "Start story for New Asgard in earth.txt"
```

```output
[main 9b26458] Start story for New Asgard in earth.txt
 1 file changed, 1 insertion(+)
 create mode 100644 earth.txt
```

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a commit
(or revision) and its short identifier is `9b26458`
(Your commit will have another identifier.)

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch a VS Code window (or whatever other editor we configured as `core.editor`)
so that we can write a longer message.

[Good commit messages][commit-messages] start with a brief (<50 characters) summary of
changes made in the commit.  If you want to go into more detail, add
a blank line between the summary line and your additional notes.

If we run `git status` now:

```bash
$ git status
```

```output
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

It tells us everything is up to date.
If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`:

```bash
$ git log
```

```output
commit 9b26458f5d229d48be61023bcb510f8beb3f13db (HEAD -> main)
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 20:18:55 2025 -0400

    Start story for New Asgard in earth.txt

commit f537d84c6ef9b6d988f642400b2017f855f9aaa1 (origin/main, origin/HEAD)
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 18:34:45 2025 -0400

    Initial commit
```

`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes
the commit's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the commit's author,
when it was created,
and the log message Git was given when the commit was created

## Make more changes to the file

Now suppose Loki records another event in the file.

Click back into the `earth.txt` file, and add a second line:

```output
Thor defends New Asgard from invaders.
Thor and Valkyrie coordinate a counterattack.

```

Save the file (make sure to have a newline at the end!).

When we run `git status` now,
it tells us that a file it already knows about has been modified:

```bash
$ git status
```

```output
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   earth.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now. It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:

```bash
$ git diff
```

```output
diff --git a/earth.txt b/earth.txt
index 0b592c6..d27fc77 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1 +1,2 @@
 Thor defends New Asgard from invaders.
+Thor and Valkyrie coordinate a counterattack.
```

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `0b592c6` and `d27fc77` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line.

After reviewing our change, it's time to commit it:

```bash
$ git commit -m "Implement counterattack strategy"
```

```output
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   earth.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that:

```bash
$ git add earth.txt
$ git commit -m "Implement counterattack strategy"
```

```output
[main ee67c8b] Implement counterattack strategy
 1 file changed, 1 insertion(+)
```

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.

To allow for this,
Git has a special *staging area*
where it keeps track of things that have been added to
the current changeset
but not yet committed.

:::::::::::::::::::::::::: callout

If you think of Git as taking snapshots of changes over the life of a project,
`git add` specifies *what* will go in a snapshot
(putting things in the staging area),
and `git commit` then *actually takes* the snapshot, and
makes a permanent record of it (as a commit).
If you don't have anything staged when you type `git commit`,
Git will prompt you to use `git commit -a` or `git commit --all`,
which is kind of like gathering *everyone* for the picture!
However, it's almost always better to
explicitly add things to the staging area, because you might
commit changes you forgot you made. (Going back to snapshots,
you might get the extra with incomplete makeup walking on
the stage for the snapshot because you used `-a`!)
Try to stage things manually,
or you might find yourself searching for "git undo commit" more
than you would like!

::::::::::::::::::::::::::

![The Git Staging Area](fig/git-staging-area.svg)

## Using the Source Control pane in VS Code

Let's watch as our changes to a file move from our editor
to the staging area and into long-term storage.
First, we'll add another line to the file:


```output
Thor defends New Asgard from invaders.
Thor and Valkyrie coordinate a counterattack.
Thor reunites with Jane Foster at the sanctuary.

```

Save the file (with a newline at the end!).

Switch from the Explorer pane view to the Source Control pane view in VS Code.

Under "Changes", you should see your `earth.txt` file. Click the file.

In your Terminal window, type the command:

```bash
$ git diff
```

```output
diff --git a/earth.txt b/earth.txt
index d27fc77..8938f14 100644
--- a/earth.txt
+++ b/earth.txt
@@ -1,2 +1,3 @@
 Thor defends New Asgard from invaders.
 Thor and Valkyrie coordinate a counterattack.
+Thor reunites with Jane Foster at the sanctuary.
```

The `git diff` command is accomplishing the same thing as clicking on the file under "Changes": that we've added one line to the end of the file
(shown with a `+` in the first column).

In the Source Control pane, click the `+` icon next to the `earth.txt` file. 
The `earth.txt` file gets moved to the "Saved Changes" section.

Clicking the `+` icon accomplished the same thing as typing `git add earth.txt` in the terminal.

Now, let's save our changes. We could use the Terminal to commit our changes:

```bash
$ git commit -m "Complete story with Thor-Jane reunion"
```

```output
[main 2f2d364] Complete story with Thor-Jane reunion
 1 file changed, 1 insertion(+)
```

Or, we can type the commit message "Complete story with Thor-Jane reunion" in the "Message" box and click "Commit".

Let's check our status:

```bash
$ git status
```

```output
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

and look at the history of what we've done so far:

```bash
$ git log
```

```output
commit 2f2d364f559efb1101647591d9fbf2cc30ade8bb (HEAD -> main)
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 20:29:51 2025 -0400

    Complete story with Thor-Jane reunion

commit ee67c8b551612e09be46c97726866d04c7b0d785
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 20:24:35 2025 -0400

    Implement counterattack strategy

commit 9b26458f5d229d48be61023bcb510f8beb3f13db
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 20:18:55 2025 -0400

    Start story for New Asgard in earth.txt

commit f537d84c6ef9b6d988f642400b2017f855f9aaa1 (origin/main, origin/HEAD)
Author: Loki Odinson <loki.odinson@tva.org>
Date:   Sat May 17 18:34:45 2025 -0400

    Initial commit
```

::::::::::::::::::::::::: challenge

Look back at the Source Control pane. Where can you see a GUI representation of this log?

::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `git status` shows the status of a repository.
- Files can be stored in a project's working directory (which users see), the staging area (where the next commit is being built up) and the local repository (where commits are permanently recorded).
- `git add` puts files in the staging area.
- `git commit` saves the staged content as a new commit in the local repository.
- Always write a log message when committing changes.

::::::::::::::::::::::::::::::::::::::::::::::::::

[commit-messages]: https://chris.beams.io/posts/git-commit/
