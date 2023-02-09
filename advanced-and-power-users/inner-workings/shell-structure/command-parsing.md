---
description: How command parsing works
---

# 🗜 Command Parsing

Once the `GetLine()` function got your input, it attempts to split any command with the semicolon between them, like:

```
command1 arg1 arg2 ; command2 arg3 arg4
```

Any command that starts with either a space or a hashtag will be ignored as a comment, like:

```
 comment
#comment
```

The first word is a command, and all words following it in a single command text are the series of arguments. These words then get split to arguments (without the switch indicator `-switch`) and switches (arguments that come after the dash) using the `ProvidedCommandArgumentsInfo` class, though it does much more than that.

This class contains these variables:

* `Command`: Target command
* `ArgumentsText`: Provided arguments and switches
* `ArgumentsList`: Array of arguments without the switches
* `SwitchesList`: Array of switches
* `RequiredArgumentsProvided`: Checks to see if the arguments are provided or not

After the above class constructor is called, the shell attempts to execute a mod or alias command, if found. Else, the built-in command is going to be executed. It checks for these redirection flags:

* `>>`: Redirects the output to a file, overwriting the target file
* `>>>`: Redirects the output to a file, appending to the target file
* `|SILENT|`: Redirects the output to a null console driver, which means no output

If these flags are found, the shell sets the console driver as appropriate.

The shell then checks to see if the command is executable with the current user permissions. If the command is a strict command (`CommandFlags.Strict`) and the user has been granted either the administrator status or the `PermissionTypes.RunStrictCommands` permission, or if the command is not a strict command, then the shell is able to execute the specified command.

However, if the maintenance mode is on and the command is set not to run on maintenance mode (`CommandFlags.NoMaintenance`), then the shell bails from executing the command, with the message that it can't run in maintenance mode.

Finally, the command executor thread is fired up with the `ExecuteCommandParameters` instance to hold command execution parameters for the same thread. The thread is then started.

However, the command executor checks for these:

* If the provided command is a UESH script, the shell invokes a script executor.
* If the command is an external program found in the shell lookup path, which is usually `$PATH`, the shell attempts to scan these directories for the program and execute it.
* If the command is an internal command, it creates a separate thread for the command.

## Switch Management

There is a static class dedicated to managing the switches, called SwitchManager. It allows you to manage the switches with the values. There are two functions that specialize in getting the switch values: `GetSwitchValues` and `GetSwitchValue`.

The first function returns the list of switches with their values stored in a tuple, and the second function returns the switch value for a specified switch or a blank value if not found.

{% hint style="info" %}
You can always use these functions with the `SwitchesOnly` array found in the `Execute()` function in the `CommandBase` class.
{% endhint %}
