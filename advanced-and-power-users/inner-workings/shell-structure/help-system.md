---
description: Inner workings of the help system
---

# ❔ Help System

The help system is what every shell uses, invoked by the unified `help` command available for every type of shell. The function responsible for showing help entries or command usage and some extra help is `HelpSystem.ShowHelp()` in the `KS.Shell.ShellBase.Commands` namespace. Explore with us the mechanics of the help system below.

## General help

When the user requests the `help` command in any shell, the above function gets called, querying the current shell type (`Shell.CurrentShellType`) as discussed previously.

The function gets all the commands, including the unified ones, from the command type, but hides all the hidden commands (commands that are flagged with the `CommandFlags.Hidden` flag). It also takes care of the modded and aliased commands.

The help system then prints the list of commands to the console.

## Command help

If the user specified a command when calling the `help` command, the help system extracts the help definition and all the command usages.

It extracts from these values found in the `CommandInfo` class:

* `HelpDefinition`: The brief summary of what the command does
* `CommandArgumentInfo.HelpUsages`: Defines the command usages
