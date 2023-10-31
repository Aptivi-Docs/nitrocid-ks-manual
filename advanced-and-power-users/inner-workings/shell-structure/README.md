---
description: Explaining the inner workings of all the kernel shells
---

# 🐚 Shell Structure

Kernel shells can be built by implementing two different interfaces and base classes. Why two? Because the shell handler relies on:

* `BaseShell` and `IShell`: To hold shell type and initialization code
* `BaseShellInfo` and `IShellInfo`: To hold shell commands and the base shell

## Shell Handler

The shell handler, `ShellManager`, uses the available shell list, which holds the `BaseShellInfo` abstract class, to manipulate with that shell. That class can be get, depending on the needed type, with the `ShellManager.GetShellInfo()` function in the ︎`KS.Shell` namespace.

The shell handler also contains two properties: `CurrentShellType` and `LastShellType`. The former property holds the current shell type, which can be used with the shell management functions. The latter property holds the last shell type, which is usually the shell that you exited. However, there are three cases:

* If there are no shells in the shell stack, it returns the primary `Shell`
* If there is only one shell in the stack, it returns the current shell as the last one
* If there are two or more shells in the stack, it returns the last shell type

Additionally, when `GetLine()` is called, it sets Terminaux's reader history to point to the shell's history list. After it's done getting the input, it reverts back to the `General` history buffer. They are loaded on boot and saved on shutdown or reboot.

{% hint style="info" %}
You can force a reload on the history by using the `loadhistories` command across all the shells.

You can manually save the history list for all the shells using the `savehistories` command.
{% endhint %}

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

* All shells **must** call the `ShellManager.GetLine()` function, which usually is adaptive to your shell type. This is the below example code inside the shell initialization code to illustrate this:

```csharp
while (!Bail)
{
    ShellManager.GetLine();
}
```

* All shells **must** also handle both the `ThreadInterruptedException`, which must set `Bail` to `true`, and the general exceptions, which must call `continue` after dumping the exception to the debugger or to the console. For example, the below example code, inside the `InitializeShell()` function:

```csharp
while (!Bail)
{
    try
    {
        ShellManager.GetLine();
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

While `ShellManager.GetLine()` prompts for input, it decides which shell preset, `PromptPresetBase`, is used according to the list of presets, `ShellPresets`, that **should** make a new prompt preset class that you made for your shell.

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
public override string PresetPrompt =>
    PresetPromptBuilder();
internal override string PresetPromptBuilder()
```

Optionally, these variables can be overridden:

* `PresetPromptCompletion`: **Read-only property.** Usually calls the overridable internal function `PresetPromptCompletionBuilder()`. If it's simple, overriding it with a string is enough.

```csharp
public override string PresetPromptCompletion =>
    PresetPromptCompletionBuilder();
internal override string PresetPromptCompletionBuilder()
```

* `PresetPromptShowcase`: **Read-only property.** Usually calls the overridable internal function `PresetPromptBuilderShowcase()`. If it's simple, overriding it with a string is enough.

```csharp
public override string PresetPromptShowcase =>
    PresetPromptBuilderShowcase();
internal override string PresetPromptBuilderShowcase()
```

* `PresetPromptCompletionShowcase`: **Read-only property.** Usually calls the overridable internal function `PresetPromptCompletionBuilderShowcase()`. If it's simple, overriding it with a string is enough.

```csharp
public override string PresetPromptCompletionShowcase =>
    PresetPromptCompletionBuilderShowcase();
internal override string PresetPromptCompletionBuilderShowcase()
```

{% hint style="warning" %}
Since the `Showcase` versions of the properties are meant to simulate how the preset would look in the real-world, you shouldn't try to access any external asset, especially those that the non-showcase properties use.

The easiest way to avoid using these assets is to make up things, such as `database.sqlite` for the SQL shell.
{% endhint %}

## Shell Information

Every `BaseShell` class you create must accompany it with a separate class that implements the `BaseShellInfo` and `IShellInfo` classes, as in below:

```csharp
internal class YourShellInfo : BaseShellInfo, IShellInfo
```

This is where your commands get together by overriding the `Commands` variable with the new dictionary containing all your commands, like below (in the UESH shell):

```csharp
public override Dictionary<string, CommandInfo> Commands => new()
{
    { "adduser",
        new CommandInfo("adduser", /* Localizable */ "Adds users",
            new[] {
                new CommandArgumentInfo(new[]
                {
                    new CommandArgumentPart(true, "username"),
                    new CommandArgumentPart(false, "password"),
                    new CommandArgumentPart(false, "confirm"),
                }, Array.Empty<SwitchInfo>())
            }, new AddUserCommand(), CommandFlags.Strict)
    },
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

By default, your shells don't accept network connections. To make them accept network connections, you must override the `AcceptsNetworkConnection` so that it holds the value of `true` instead of `false`. This causes the network connection selector, especially `OpenConnectionForShell()` which can be invoked in your networked shell launch code in your command class, to be able to acknowledge your shell.

```csharp
public override bool AcceptsNetworkConnection => true;
```

You'll have to adapt your shell to take the first argument, `ShellArgs[0]`, as the network connection instance in your `Shell` instance. For example, we've done this to the FTP shell and shell info instances:

<pre class="language-csharp" data-title="FTPShell.cs" data-line-numbers><code class="lang-csharp">public override void InitializeShell(params object[] ShellArgs)
{
    // Parse shell arguments
<strong>    NetworkConnection ftpConnection = (NetworkConnection)ShellArgs[0];
</strong><strong>    FtpClient clientFTP = (FtpClient)ftpConnection.ConnectionInstance;
</strong>
    // Finalize current connection
    FTPShellCommon.clientConnection = ftpConnection;
</code></pre>

<pre class="language-csharp" data-title="FTPShellInfo.cs" data-line-numbers><code class="lang-csharp">internal class FTPShellInfo : BaseShellInfo, IShellInfo
{
    (...)
<strong>    public override bool AcceptsNetworkConnection => true;
</strong>}
</code></pre>

## Command Info

Each command you define in your shell must provide a new instance of the `CommandInfo` class holding details about the specified command. The new instance of the class can be made using the constructor defined below:

```csharp
public CommandInfo(string Command, string HelpDefinition, CommandArgumentInfo[] CommandArgumentInfo, BaseCommand CommandBase, CommandFlags Flags = CommandFlags.None)
```

where:

* `Command`: The command
* `HelpDefinition`: The brief summary of what the command does
* `CommandArgumentInfo`: Array of argument information about your command
* `CommandBase`: An instance of the `BaseCommand` containing command execution information
* `CommandFlags`: All command flags

To implement `CommandArgumentInfo`, call the constructor either with no parameters, which implies that there is no argument required to run this command, or with the following options listed below.

```csharp
public CommandArgumentInfo()
public CommandArgumentInfo(bool AcceptsSet)
public CommandArgumentInfo(CommandArgumentPart[] Arguments)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, bool AcceptsSet)
public CommandArgumentInfo(SwitchInfo[] Switches)
public CommandArgumentInfo(SwitchInfo[] Switches, bool AcceptsSet)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, SwitchInfo[] Switches)
public CommandArgumentInfo(CommandArgumentPart[] Arguments, SwitchInfo[] Switches, bool AcceptsSet)
```

where:

* `Arguments`: Defines the command arguments
* `Switches`: Defines the command switches
* `AcceptsSet`: Whether to accept the `-set` switch

For `CommandArgumentPart` instances, consult the below constructor to create an array of `CommandArgumentPart` instances when defining your commands:

```csharp
public CommandArgumentPart(bool argumentRequired, string argumentExpression, Func<string[], string[]> autoCompleter = null, bool isNumeric = false, string exactWording = null)
```

where:

* `argumentRequired`: Is this argument part required?
* `argumentExpression`: Command argument expression
* `autoCompleter`: Auto completion function delegate
  * The first `string[]` denotes the list of last passed arguments
  * The second `string[]` (output) denotes the suggestions returned
* `isNumeric`: Whether this argument part accepts numeric values only
* `exactWording`: If not empty, the user must write this wording for this argument to be satisfied

{% hint style="info" %}
When it comes to auto-completion, if you press TAB on any of the argument positions, the shell will select the following completers as appropriate:

* If the auto completer is specified, then, regardless of whether the expression represents the selection (expressions containing the slash `/` character) or not, the auto completer specified in the constructor will be called.
* If the auto completer is not specified, then it will go through the following completers:
  * The shell goes through the list of known completion expressions according to the argument expression, which are the following:
    * `user`, `username`: List of usernames
    * `group`, `groupname`: List of groups
    * `modname`: List of kernel mods
    * `splashname`: List of splashes
    * `saver`: List of screensavers
    * `theme`: List of themes
    * `$variable`: List of UESH variables
    * `perm`: List of permission types
    * `cmd`, `command`: List of all available commands
  * If the expression is not listed in any of the known expressions list, it'll check for the selection indicator characters (the slash `/` key).
    * For example, the `true/false` expression will generate an autocompleter that completes the two words: `true` and `false`.
  * In case there is none, the shell will use the default auto completer, which fetches possible files and folders on your current working directory.
{% endhint %}

{% hint style="success" %}
Usually, there is no need for you to cut the string to the required position; the shell does it to every single autocomplete result that is given.
{% endhint %}

### Command argument part with options

In case you want to expressively specify the options without having to use default values for all parameters to set a certain parameter, you can use the `CommandArgumentPartOptions` overload:

```csharp
public CommandArgumentPart(bool argumentRequired, string argumentExpression, CommandArgumentPartOptions options)
```

## Switch Info

For `SwitchInfo` instances, consult the below constructors to create an array of `SwitchInfo` instances when defining your commands:

```csharp
public SwitchInfo(string Switch, string HelpDefinition)
public SwitchInfo(string Switch, string HelpDefinition, SwitchOptions options)
public SwitchInfo(string Switch, string HelpDefinition, bool IsRequired = false, bool ArgumentsRequired = false, string[] conflictsWith = null, int optionalizeLastRequiredArguments = 0)
```

{% hint style="info" %}
You can access the switch options using the `Options` property. The existing properties, like `IsRequired`, are proxies to that property, but are to stay for compatibility.

Try to use the second overload if you want to specify the options, if possible. This allows you to be more expressive in your mod command definition code, making it more readable.
{% endhint %}

## Base Command

The base command is required to be implemented, since it contains overridable command execution code. Your command must implement the command base class below:

```csharp
class YourCommand : BaseCommand, ICommand
```

The only function that you need to override is `Execute()`, which you can override like below:

```csharp
public override int Execute(CommandParameters parameters, ref string variableValue)
```

To support dumb consoles that don't support positioning or complex console functions, you can override `ExecuteDumb()`:

```csharp
public override int ExecuteDumb(CommandParameters parameters, ref string variableValue)
```

Additionally, you can override the extra help function, `HelpHelper()`, like this:

```csharp
public override void HelpHelper()
```

{% hint style="info" %}
If you want to support redirection or wrapping, you must either take dumb console support into account on the `Execute()` function by not calling any of the below console wrappers, or you must override the `ExecuteDumb()` function shown above to be compatible with the dumb consoles.

The following wrappers should not be called (explicitly and implicitly) on that function:

* `CursorLeft` (set)
* `CursorTop` (set)
* `ForegroundColor`
* `BackgroundColor`
* `CursorVisible`
* `OutputEncoding`
* `InputEncoding`
* `KeyAvailable`
* `Beep()`
* `Clear()`
* `OpenStandardError()`
* `OpenStandardInput()`
* `OpenStandardOutput()`
* `ReadKey()`
* `ResetColor()`
* `SetCursorPosition()`
* `SetOut()`
{% endhint %}

### Registering your command

In order for your command to be usable, your mods are now required to register the commands manually using a function that helps doing this. That function is defined in the `CommandManager` class.

{% code title="CommandManager.cs" lineNumbers="true" %}
```csharp
public static void RegisterCustomCommand(ShellType ShellType, CommandInfo commandBase)
public static void RegisterCustomCommand(string ShellType, CommandInfo commandBase)
public static void RegisterCustomCommands(ShellType ShellType, CommandInfo[] commandBases)
public static void RegisterCustomCommands(string ShellType, CommandInfo[] commandBases)
```
{% endcode %}

Similarly, if your mod is going to stop, you must unregister all your mod commands, including those that it created in the middle of the kernel uptime. You can use the following functions:

{% code title="CommandManager.cs" lineNumbers="true" %}
```csharp
public static void UnregisterCustomCommand(ShellType ShellType, string commandName)
public static void UnregisterCustomCommand(string ShellType, string commandName)
public static void UnregisterCustomCommands(ShellType ShellType, string[] commandNames)
public static void UnregisterCustomCommands(string ShellType, string[] commandNames)
```
{% endcode %}

If you've registered your commands correctly, the `help` command list should list your mod command that you've registered using one of the `RegisterCustomCommand` functions.

{% hint style="info" %}
If you're migrating your mods, your mod code can still contain the old `Commands` list, but you must use the following properties:

* `Commands.Keys` (command names for unregistration)
* `Commands.Values` (command info instances for registration)

Since Nitrocid no longer uses this list, we recommend that you use it as a mutable list of commands just for your mods, since you could be generating commands and registering them.
{% endhint %}

### Setting command values

There is a special switch called `set` that allows your command to set the final variable value to any value. For example, if you run `calc` with the `-set` switch to a variable called `result`, that variable will be set to an output value (in this case an arithmetic result) using the `variableValue` argument.

To take advantage of the feature, just write the following code at the end of `Execute()`:

```csharp
variableValue = myValue;
```

...where `myValue` is a string representation of the resulting value that the command produces. A real-world example of this is provided (from the `echo` command code):

```csharp
string result = PlaceParse.ProbePlaces(StringArgs);
TextWriterColor.Write(result);
variableValue = result;
```

### Command flags

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

{% hint style="info" %}
`SettingVariable` is obsolete. Please use the AcceptsSet parameter when making a new CommandArgumentInfo.
{% endhint %}

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
