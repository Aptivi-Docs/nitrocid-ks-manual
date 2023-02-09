---
description: Explaining the inner workings of all the kernel shells
---

# 🐚 Shell Structure

Kernel shells can be built by implementing two different interfaces and base classes. Why two? Because the shell handler relies on:

* `BaseShell` and `IShell`: To hold shell type and initialization code
* `BaseShellInfo` and `IShellInfo`: To hold shell commands and the base shell

## Shell Handler

The shell handler, `Shell`, uses the available shell list, which holds the `BaseShellInfo` abstract class, to manipulate with that shell. That class can be get, depending on the needed type, with the `Shell.GetShellInfo()` function in the ︎`KS.Shell` namespace.

The shell handler also contains two properties: `CurrentShellType` and `LastShellType`. The former property holds the current shell type, which can be used with the shell management functions. The latter property holds the last shell type, which is usually the shell that you exited. However, there are three cases:

* If there are no shells in the shell stack, it returns the primary `Shell`
* If there is only one shell in the stack, it returns the current shell as the last one
* If there are two or more shells in the stack, it returns the last shell type

## Base Shell

The `BaseShell` abstract class, which your shell must override, contains the shell type name (`ShellType`), the flag to bail from the shell (`Bail`), and the shell initialization code with the shell arguments (`InitializeShell()`).

```csharp
public class YourShell : BaseShell, IShell
```

The shell initialization code usually waits for the `Bail` value to become `true` (the shell requested bailing, usually done by exiting the shell using the `exit` universal command), as in the below example code.

```csharp
public override void InitializeShell(params object[] ShellArgs)
{
    while (!Bail)
    {
        // Shell code
    }
}
```

While it's waiting for this to happen, the shell does what it's programmed to do, but in two conditions:

* All shells **must** call the `Shell.GetLine()` function, which usually is adaptive to your shell type. This is the below example code inside the shell initialization code to illustrate this:

```csharp
while (!Bail)
{
    Shell.GetLine();
}
```

* All shells **must** also handle both the `ThreadInterruptedException`, which must set `Bail` to `true`, and the general exceptions, which must call `continue` after dumping the exception to the debugger or to the console. For example, the below example code, inside the `InitializeShell()` function:

```csharp
while (!Bail)
{
    try
    {
        Shell.GetLine();
    }
    catch (ThreadInterruptedException)
    {
        Flags.CancelRequested = false;
        Bail = true;
    }
    catch (Exception ex)
    {
        DebugWriter.WriteDebugStackTrace(ex);
        TextWriterColor.Write(Translate.DoTranslation("There was an error in the shell.") + CharManager.NewLine + "Error {0}: {1}", true, KernelColorType.Error, ex.GetType().FullName, ex.Message);
        continue;
    }
}
```

The shell registration is required once you're done implementing the shell and all its required values, which will show you how to implement them in the next three pages. The function responsible for this action is `ShellTypeManager.RegisterShell()` in the `KS.Shell.ShellBase.Shells` namespace.

{% hint style="danger" %}
Be sure to unregister your shell using the `UnregisterShell()` function, or the shell registry function will not update your `BaseShellInfo` class in the available shell lists!
{% endhint %}

## Shell Presets

While `Shell.GetLine()` prompts for input, it decides which shell preset, `PromptPresetBase`, is used according to the list of presets, `ShellPresets`, that **should** make a new prompt preset class that you made for your shell.

`CurrentPreset` specifies the current `PromptPresetBase` class, which is usually found in the `ShellPresets` list. It usually calls the `PromptPresetManager.CurrentPresets[ShellType]` variable.

{% hint style="warning" %}
The first preset **should** implement a preset called `Default` in the `ShellPresets` dictionary.
{% endhint %}

`PromptPresetManager.SetPreset()` queries both the shell pre-defined presets, `ShellPresets`, and the custom presets, `CustomShellPresets`. After that, it sets the preset to the specified preset in the internal `CurrentPresets`.

Every preset must implement a base class, `PromptPresetBase` and `IPromptPreset`, as in below:

```csharp
public class YourDefaultPreset : PromptPresetBase, IPromptPreset
```

The only essential values that you **must** override in your shell preset class are:

* `PresetName`: **Read-only property.** The shell preset name. If this preset is your first preset, it must be `Default`.

```csharp
public override string PresetName { get; } = "Default";
```

* `PresetPrompt`: **Read-only property.** Usually calls the overridable internal function `PresetPromptBuilder()`. If it's simple, overriding it with a string is enough.

```csharp
public override string PresetPrompt => PresetPromptBuilder();

internal override string PresetPromptBuilder()
```

Optionally, these variables can be overridden:

* `PresetPromptCompletion`: **Read-only property.** Usually calls the overridable internal function `PresetPromptCompletionBuilder()`. If it's simple, overriding it with a string is enough.

```csharp
public override string PresetPromptCompletion => PresetPromptCompletionBuilder();

internal override string PresetPromptConpletionBuilder()
```

## Shell Information

Every `BaseShell` class you create must accompany it with a separate class that implements the `BaseShellInfo` and `IShellInfo` classes, as in below:

```csharp
internal class YourShellInfo : BaseShellInfo, IShellInfo
```

This is where your commands get together by overriding the `Commands` variable with the new dictionary containing all your commands, like below (in the UESH shell):

```csharp
public override Dictionary<string, CommandInfo> Commands => new()
{
    { "adduser", new CommandInfo("adduser", ShellType, "Adds users", new CommandArgumentInfo(new[] { "<userName> [password] [confirm]" }, true, 1), new AddUserCommand(), CommandFlags.Strict) },
    (...)
};
```

In addition, you can override the `ShellPresets` class with a new dictionary containing all the presets for your shell, like below:

```csharp
public override Dictionary<string, PromptPresetBase> ShellPresets => new()
{
    { "Default", new DefaultPreset() }
};
```

`ShellBase`, however, must be overridden with an instance of your shell in this form:

```csharp
public override BaseShell ShellBase => new YourShell();
```

Additionally, `CurrentPreset` must be overridden with a variable that queries your shell type with the `CurrentPresets` variable as in below:

```csharp
public override PromptPresetBase CurrentPreset => PromptPresetManager.CurrentPresets[ShellType];
```

The `ShellType` variable found within the `BaseShellInfo` class is a wrapper for the `ShellBase.ShellType` variable for easier access. It's not overridable and is defined like this:

```csharp
public string ShellType => ShellBase.ShellType;
```

## Command Info

Each command you define in your shell must provide a new instance of the `CommandInfo` class holding details about the specified command. The new instance of the class can be made using the constructor defined below:

```csharp
public CommandInfo(string Command, string Type, string HelpDefinition, CommandArgumentInfo CommandArgumentInfo, BaseCommand CommandBase, CommandFlags Flags = CommandFlags.None)
```

where:

* `Command`: The command
* `Type`: Your shell type
* `HelpDefinition`: The brief summary of what the command does
* `CommandArgumentInfo`: Argument information about your command
* `CommandBase`: An instance of the `BaseCommand` containing command execution information
* `CommandFlags`: All command flags

To implement `CommandArgumentInfo`, call the constructor either with no parameters, which implies that there is no argument required to run this command, or with the following options listed below.

```csharp
public CommandArgumentInfo(string[] HelpUsages, bool ArgumentsRequired, int MinimumArguments, Func<string, int, char[], string[]> AutoCompleter = null)
```

where:

* `HelpUsages`: Defines the command usages
* `ArgumentsRequired`: Specifies whether the arguments are required
* `MinimumArguments`: Specifies how many arguments are required to execute the command
* `AutoCompleter`: **Optional.** Auto completer function that returns an array of suggestions

The base command is required to be implemented, since it contains overridable command execution code. Your command must implement the command base class below:

```csharp
class YourCommand : BaseCommand, ICommand
```

The only function that you need to override is `Execute()`, which you can override like below:

```csharp
public override void Execute(string StringArgs, string[] ListArgsOnly, string[] ListSwitchesOnly)
```

Additionally, you can override the extra help function, `HelpHelper()`, like this:

```csharp
public override void HelpHelper()
```

Finally, the command flags (`CommandFlags`) can be defined. One or more of the command flags can be defined using the OR (`|`) operator when defining the command flags. These flags are available:

* `Strict`: The command is strict, meaning that it's only available for administrators.
  * The flag value is 1
* `NoMaintenance`: This command can't run in maintenance mode.
  * The flag value is 2
* `Obsolete`: The command is obsolete.
  * The flag value is 4
* `SettingVariable`: The command is setting a UESH variable.
  * The flag value is 8
* `RedirectionSupported`: Redirection is supported, meaning that all the output to the commands can be redirected to a file.
  * The flag value is 16
* `Wrappable`: This command is wrappable to pages.
  * The flag value is 32
* `Hidden`: This command can be executed, but not shown in command list generated by help.
  * The flag value is 64

## More?

For information about the help system and how it works, consult the below page:

{% content-ref url="help-system.md" %}
[help-system.md](help-system.md)
{% endcontent-ref %}

For command parsing, click the below button:

{% content-ref url="command-parsing.md" %}
[command-parsing.md](command-parsing.md)
{% endcontent-ref %}

For shell scripting, click the below button:

{% content-ref url="shell-scripting.md" %}
[shell-scripting.md](shell-scripting.md)
{% endcontent-ref %}
