---
description: How command parsing works
---

# 🗜 Command Parsing

Once the `GetLine()` function gets your input, it attempts to split any command with the semicolon between them, like:

```
command1 arg1 arg2 ; command2 arg3 arg4
```

Any command that starts with either a space or a hashtag will be ignored as a comment, like:

```
 comment
#comment
```

The first word is a command, and all words following it in a single command text are the series of arguments. These words then get split to arguments (without the switch indicator `-switch`) and switches (arguments that come after the dash) using the `ProvidedArgumentsInfo` class, though it does much more than that.

This class contains these variables:

* `Command`: Target command
* `ArgumentsText`: Provided arguments and switches
* `ArgumentsList`: Array of arguments without the switches
* `SwitchesList`: Array of switches
* `RequiredArgumentsProvided`: Checks to see if the arguments are provided or not
* `RequiredSwitchesProvided`: Checks to see if the required switches are provided or not
* `RequiredSwitchArgumentsProvided`: Checks to see if the required switch arguments are provided or not

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

The `ExecuteCommandWrapped()` function allows you to execute a command in wrapped mode from your mod commands. However, your mods must execute a command that has one of the flags, called `CommandFlags.Wrappable`, otherwise, this function prints the list of wrappable commands.

## Switch Management

There is a static class dedicated to managing the switches, called SwitchManager. It allows you to manage the switches with the values. There are two functions that specialize in getting the switch values: `GetSwitchValues()` and `GetSwitchValue()`.

The first function returns the list of switches with their values stored in a tuple, and the second function returns the switch value for a specified switch or a blank value if not found.

{% hint style="info" %}
You can always use these functions with the `SwitchesOnly` array found in the `Execute()` function in the `CommandBase` class.
{% endhint %}

The switches can be set to conflict with each other by passing an array of incompatible switches to the SwitchInfo constructor, specifically the last parameter, `conflictsWith`. However, each switch to be conflicted must set their `conflictsWith` arrays to the opposing switches.

The switches can also be set not to accept any value by setting the `AcceptsValues` argument to `false`. It will cause parsing to fail once the value in such switches are encountered, stating that such switches don't accept any value.

For example, if you want a command to have three switches (`-s`, `-t`, `-u`) that conflict with each other, you can specify three SwitchInfo instances with the following properties (assuming that you've already set the `HelpDefinition`, `IsRequired`, and `ArgumentsRequired` parameters):

* `-s`
  * Switch: `s`
  * ConflictsWith: `new string[] { "t", "u" }`
* `-t`
  * Switch: `t`
  * ConflictsWith: `new string[] { "s", "u" }`
* `-u`
  * Switch: `u`
  * ConflictsWith: `new string[] { "s", "t" }`

{% hint style="warning" %}
You may only specify the switch names without the dash in the `Switch` argument and the `ConflictsWith` argument.
{% endhint %}

{% hint style="danger" %}
Be sure that you put all the conflicts in the above form for each conflicting `SwitchInfo`. Failure to do this may cause the UESH shell to believe that they don't conflict, while they do. For example, we have an edit command that contains three conflicting switches (`-json`, `-hex`, and `-text`) that is implemented below:

{% code title="UESHShellInfo.cs" lineNumbers="true" %}
```csharp
{ "edit",
    new CommandInfo("edit", ShellType, /* Localizable */ "Edits a file",
        new[] {
            new CommandArgumentInfo(new[] { "file" }, new[] {
                new SwitchInfo("text", /* Localizable */ "Forces text mode", false, false, new string[] { "hex", "json" }, 0, false),
                new SwitchInfo("hex", /* Localizable */ "Forces hex mode", false, false, new string[] { "text", "json" }, 0, false),
                new SwitchInfo("json", /* Localizable */ "Forces JSON mode", false, false, new string[] { "text", "hex" }, 0, false)
            }, true, 1)
        }, new EditCommand())
},
```
{% endcode %}
{% endhint %}

As for the switches that cause some or all arguments to be omittable (optional), you can indicate so in the constructor of your switch. The `optionalizeLastRequiredArguments` argument in the constructor specifies how many arguments are going to be made optional starting from the last argument in the list.

For example, if this parameter was set to 1 and you've defined three required arguments, which are named below:

* `Arg1`
* `Arg2`
* `Arg3`

Then, this will set `Arg3` to be omittable, which means that the user doesn't have to set the value for this argument in order for the command to execute.

{% hint style="info" %}
A real-world example is the `weather` command. It contains an switch, `-list`, which omits the last 2 arguments, which causes this command to be executable with just `weather -list`. Its `SwitchInfo` is defined below:

```csharp
new SwitchInfo("list", "Shows all the available cities", false, false, null, 2, false)
```
{% endhint %}
