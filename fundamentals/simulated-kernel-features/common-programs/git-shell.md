---
description: Git Shell in your hands
---

# 👩💻 Git Shell

Git is a version controlling system that allows you to manage your project source code with ease. Changes to the source code are done in batches, known as commits, which store the file changes, including their content, whether they're moved; copied; deleted; or created, their attributes, and more.

Nitrocid KS provides an add-on that allows you to use the Git shell. This is so that you can experience the Git version control system as a shell. Additionally, if you have Git installed on your system, you can run `git` in the UESH shell.

{% hint style="info" %}
If you have Extras.GitShell installed, you can launch the shell using the `gitsh` command.

Command usage:

```
gitsh <pathToRepositoryFolder>
```
{% endhint %}

### How it works

When gitsh is executed, it first verifies that the `.git` folder found inside the repository folder exists. Then, it creates a new repository instance that allows all of the Git operations to be done.

Once it's done, it checks for the following known default branch names:

* `main`
* `master`
* `dev`
* `development`
* `trunk`

{% hint style="info" %}
You can check out a specific branch using the `checkout` command.
{% endhint %}

### Available commands

Git shell provides you with a list of available commands below:

* `status`
  * Gets the current repository status by comparing the current state of the repository with the head version (usually `HEAD`).
* `checkout <branch>`
  * Checks out the repository branch (switches to target branch)
* `lsbranches`
  * Lists all branches
* `lsremotes`
  * Lists all remotes
* `stageall`
  * Stages all unstaged changes
* `stage <unstagedfile>`
  * Stages a specified unstaged file
* `unstageall`
  * Unstages all staged changes
* `unstage <stagedfile>`
  * Unstages a specified staged file
