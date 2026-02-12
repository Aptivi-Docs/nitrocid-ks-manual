---
description: Guide for upgrading 0.0.24.x mods to Beta 1
icon: up
---

# From 0.0.24.x to 0.1.0 Beta 1

This page lists all the changes that have been made from 0.0.24.x to 0.1.0 Beta 1. For upgrading your mods from 0.0.24.x directly to the 0.1.0 series, use the main upgrade page where it highlights the most important changes. We have made nine milestones prior to the first beta release.

***

## <mark style="color:$primary;">From 0.0.24.x to Milestone 1</mark>

During Milestone 1's development, we have made the following breaking changes:

<details>

<summary>Moved events to <code>KS.Kernel.Events</code></summary>

{% code title="Events.vb" lineNumbers="true" %}
```vb
Public Class Events
    Friend Property FiredEvents As New Dictionary(Of String, Object())

    'These events are fired by their Raise<EventName>() subs and are responded by their Respond<EventName>() subs.
    Public Event KernelStarted()
    Public Event PreLogin()
    Public Event PostLogin(Username As String)
    (...)
```
{% endcode %}

{% code title="EventsManager.vb" lineNumbers="true" %}
```vb
Public Function ListAllFiredEvents() As Dictionary(Of String, Object())
Public Function ListAllFiredEvents(SearchTerm As String) As Dictionary(Of String, Object())
Public Sub ClearAllFiredEvents()
```
{% endcode %}

All of the event-related code files are moved to `KS.Kernel.Events` to separate these from the actual kernel code. However, because events are part of the kernel, we prefer to put it on `KS.Kernel` namespace rather than `KS.Misc`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel events from `KS.Misc` to `KS.Kernel.Events`.
{% endhint %}

</details>

<details>

<summary>Moved <code>PlatformDetector</code> to <code>KS.Kernel.KernelPlatform</code></summary>

{% code title="PlatformDetector.vb" lineNumbers="true" %}
```vb
Public Module PlatformDetector
```
{% endcode %}

It has come to the conclusion that `PlatformDetector` is now promoted to the Kernel namespace under the name `KernelPlatform` so you can access it under the `KS.Kernel` namespace.

{% hint style="info" %}
Change the namespace declaration to refer to kernel platform code from `KS.Misc` to `KS.Kernel.KernelPlatform`.
{% endhint %}

</details>

<details>

<summary>Separated the MOTD and MAL parsers</summary>

{% code title="MOTDParse.vb" lineNumbers="true" %}
```vb
Public Enum MessageType As Integer
```
{% endcode %}

MOTD and MAL parsers were unified since early versions of Nitrocid KS. However, it didn't occur to us that we need to separate them for a very long time. We took actions to separate them, effectively removing the `MessageType` enumeration.

{% hint style="info" %}
* If you want to use the MOTD parser, use the `KS.Misc.Probers.Motd` namespace to use the `MotdParse` static class methods.
* However, if you want to use the MAL parser, use the `KS.Misc.Probers.Mal` namespace to use the `MalParse` static class methods.
{% endhint %}

</details>

<details>

<summary>Moved <code>GetTerminal*</code> to <code>KernelPlatform</code></summary>

{% code title="ConsoleExtensions.vb" lineNumbers="true" %}
```vb
Public Function GetTerminalEmulator() As String
Public Function GetTerminalType() As String
```
{% endcode %}

These two functions are actually part of the terminal, and they make use of the `$TERM_PROGRAM` and `$TERM` environment variables, which are dependent on the terminal.

Since these usually are undefined in Windows, we put these functions to `KernelPlatform` to accommodate the change as platform-dependent, but we don't actually check for Linux to execute these functions, because some terminal emulators in Windows actually define these variables.

{% hint style="info" %}
Change the namespace declaration to refer to kernel terminal detection code from `KS.ConsoleBase` to `KS.Kernel.KernelPlatform`.
{% endhint %}

</details>

<details>

<summary>Moved shell common folders to <code>KS.Shell.Shells</code></summary>

This is to separate the shell code for each tool from their folders to a unified namespace, `KS.Shell.Shells`. It houses every shell for every tool. This is to make creation of built-in shells easier.

{% hint style="info" %}
This means that `*ShellCommon` modules are moved to `KS.Shell.Shells.*` and every call to that module should be redirected to that namespace. The tools, however, stays intact.
{% endhint %}

</details>

<details>

<summary>Removed <code>MakePermanent()</code></summary>

{% code title="ColorTools.vb" lineNumbers="true" %}
```vb
Public Sub MakePermanent()
```
{% endcode %}

MakePermanent used to save all the colors to kernel configuration. This function was now removed as a result of recent configuration improvements.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

</details>

<details>

<summary>Graduated <code>Configuration</code> to <code>KS.Kernel</code></summary>

{% code title="Config.vb" lineNumbers="true" %}
```vb
Namespace Misc.Configuration
```
{% endcode %}

This configuration logic was smart enough to be graduated, since it's the core function in the kernel. It's used everywhere, including the `settings` command, which is an application that lets you adjust settings on the go.

</details>

<details>

<summary>Graduated <code>FindSetting</code> and <code>CheckSettingsVariables</code></summary>

{% code title="SettingsApp.vb" lineNumbers="true" %}
```vb
Public Function FindSetting(Pattern As String, SettingsToken As JToken) As List(Of String)
Public Function CheckSettingsVariables() As Dictionary(Of String, Boolean)
```
{% endcode %}

These two functions were unrelated to the settings app, but `FindSetting()` was what `KS.Misc.Settings.SettingsApp` uses, and `CheckSettingsVariables()` was renamed to `CheckConfigVariables()` to accommodate with the graduation.

{% hint style="info" %}
You can find these methods in the `ConfigTools` module located in the `KS.Kernel.Configuration` namespace.

{% code title="ConfigTools.cs" lineNumbers="true" %}
```csharp
public static List<InputChoiceInfo> FindSetting(string Pattern, JToken SettingsToken) { }
public static Dictionary<string, bool> CheckConfigVariables() { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Moved power management functions to <code>KS.Kernel.Power</code></summary>

These power management functions were there in `KernelTools` since the earliest version of KS. Now, they're relocated to `KS.Kernel.Power`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel power code from `KS.Kernel.KernelTools` to `KS.Kernel.Power`.
{% endhint %}

</details>

<details>

<summary>Removed <code>InitPaths</code> in favor of properties</summary>

{% code title="Paths.vb" lineNumbers="true" %}
```vb
Sub InitPaths()
```
{% endcode %}

Now, we don't have to initialize paths every time we make an internal app that depends on Nitrocid KS's paths. The call to the function that gets the path, `GetKernelPath`, however won't be removed because it's widely used and is unaffected.

{% hint style="info" %}
This function is not part of the public API. Reflection calls to this function will stop working. We advice you to use the `GetKernelPath` function since it's much faster.

{% code title="Paths.cs" lineNumbers="true" %}
```csharp
public static string GetKernelPath(KernelPathType PathType) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Moved kernel update code to <code>Kernel.Updates</code></summary>

These power management functions were there in `KernelTools` since the earliest version of KS. Now, they're relocated to `KS.Kernel.Updates`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel update code from `KS.Kernel.KernelTools` to `KS.Kernel.Updates`.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 1 to Milestone 2</mark>

During Milestone 2's development, we have made the following breaking changes:

<details>

<summary>Removed <code>ListArgs</code> from <code>ICommand</code> and <code>IArgument</code></summary>

{% code lineNumbers="true" %}
```vb
'ICommand.vb
Sub Execute(StringArgs As String, ListArgs As String(), ListArgsOnly As String(), ListSwitchesOnly As String())
                                  ^^^^^^^^^^^^^^^^^^^^

'IArgument.vb
Sub Execute(StringArgs As String, ListArgs As String(), ListArgsOnly As String(), ListSwitchesOnly As String())
                                  ^^^^^^^^^^^^^^^^^^^^
```
{% endcode %}

It seems that `ListArgs` is now no longer a reliable way to check for arguments, as it could be `null` when no argument is provided. While it contains a collection of switches and arguments, it's sequential. We have separated between switches and arguments as demonstrated in both the `ListArgsOnly` and `ListSwitchesOnly` arrays.

{% hint style="info" %}
Recent changes to the shell command parsing code have allowed reliable argument and switch parsing. Use the `ListArgsOnly` and `ListSwitchesOnly` arrays to process arguments and switches.
{% endhint %}

</details>

<details>

<summary>Moved <code>GetEsc()</code> to <code>Misc.Text.CharManager</code></summary>

{% code title="Color255.vb" lineNumbers="true" %}
```vb
Public Function GetEsc() As Char
```
{% endcode %}

`GetEsc()` is now widely used for color manipulation, but we need to move it to a better place as migration to `ColorSeq` is done.

{% code title="Color255.vb" lineNumbers="true" %}
```vb
Public Module Color255
```
{% endcode %}

We have deleted `Color255` from `KS.ConsoleBase` as a result of this migration.

{% hint style="info" %}
Change the namespace declaration to refer to `GetEsc()` from `KS.ConsoleBase.Colors` to `KS.Misc.Text.CharManager`.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 2 to Milestone 3</mark>

During Milestone 3's development, we have made the following breaking changes:

<details>

<summary>Removed <code>FullArgumentList</code></summary>

{% code title="ProvidedCommandArgumentsInfo.vb" lineNumbers="true" %}
```vb
Public ReadOnly Property FullArgumentsList As String()
```
{% endcode %}

Following the removal of `ListArgs()`, we can safely remove this property.

{% hint style="info" %}
Recent changes to the shell command parsing code have allowed reliable argument and switch parsing. Use the `ListArgsOnly` and `ListSwitchesOnly` arrays to process arguments and switches.
{% endhint %}

</details>

<details>

<summary>Removed <code>ConsoleWriters.*.Write*Plain</code> in favor of the plain writers</summary>

The plain writer interfaces feel like they're a great addition to control the console writers.

{% hint style="info" %}
Use the plain writers to replace the removed plain writers from the `ConsoleWriters`.
{% endhint %}

</details>

<details>

<summary>Updated debug and notifications namespaces</summary>

We felt that moving debug-related functions to `KS.Kernel` would be more convenient, so we moved these functions to it. Also, we've renamed the notifications namespace.

{% hint style="info" %}
The below namespaces were affected in this change:

* `KS.Misc.Writers.DebugWriters` -> `KS.Kernel.Debugging`
* `KS.Network.RemoteDebug` -> `KS.Kernel.Debugging.RemoteDebug`
* `KS.Misc.Notifiers` -> `KS.Misc.Notifications`
{% endhint %}

</details>

<details>

<summary>Merged <code>ParseCmd</code> with <code>ExecuteCommand</code></summary>

{% code title="RemoteDebugCmd.vb" lineNumbers="true" %}
```vb
Sub ParseCmd(CmdString As String, SocketStreamWriter As StreamWriter, Address As String)
```
{% endcode %}

It has come to the conclusion that `ParseCmd` is now very similar to `ExecuteCommand` with treating the remote debug shell specially. This is no longer needed as `ProvidedCommandArgumentsInfo` has been provided the IP address of the target device, making `ParseCmd` redundant.

{% hint style="info" %}
This function wasn't part of the public KS API. We advice you to cease using this function and start declaring your remote debug command.
{% endhint %}

</details>

<details>

<summary>Removed <code>ExecuteRDAlias()</code></summary>

{% code title="AliasExecutor.vb" lineNumbers="true" %}
```vb
Sub ExecuteRDAlias(aliascmd As String, SocketStream As IO.StreamWriter, Address As String)
```
{% endcode %}

This function was not needed to execute aliases since there has been recent improvements to the executor in both 0.0.20.0 and 0.0.24.0.

{% hint style="info" %}
This function wasn't part of the public KS API. We advice you to cease using this function.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 3 to Milestone 4</mark>

During Milestone 4's development, we have made the following breaking changes:

<details>

<summary>Renamed debug writer function names</summary>

{% code title="DebugWriter.vb" lineNumbers="true" %}
```vb
Public Sub Wdbg(Level As DebugLevel, text As String, ParamArray vars() As Object)
Public Sub WdbgConditional(ByRef Condition As Boolean, Level As DebugLevel, text As String, ParamArray vars() As Object)
Public Sub WdbgDevicesOnly(Level As DebugLevel, text As String, ParamArray vars() As Object)
Public Sub WStkTrcConditional(ByRef Condition As Boolean, Ex As Exception)
Public Sub WStkTrc(Ex As Exception)
```
{% endcode %}

We needed to do the same thing as we've renamed `W()` to `Write()`, so we renamed the following:

* `Wdbg()` -> `WriteDebug()`
* `WdbgConditional()` -> `WriteDebugConditional()`
* `WdbgDevicesOnly()` -> `WriteDebugDevicesOnly()`
* `WStkTrcConditional()` -> `WriteDebugStackTraceConditional()`
* `WStkTrc()` -> `WriteDebugStackTrace()`

{% hint style="info" %}
You can use these functions to write debugging information in your mods to the kernel debugger. The below method signatures are provided:

{% code title="DebugWriter.cs" lineNumbers="true" %}
```csharp
public static void WriteDebug(DebugLevel Level, string text, params object[] vars) { }
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object[] vars) { }
public static void WriteDebugDevicesOnly(DebugLevel Level, string text, params object[] vars) { }
public static void WriteDebugStackTraceConditional(bool Condition, Exception Ex) { }
public static void WriteDebugStackTrace(Exception Ex) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Moved MAL and MOTD message to <code>Misc.Probers.Motd</code></summary>

{% code title="Kernel.vb" lineNumbers="true" %}
```vb
Public MOTDMessage, MAL As String
```
{% endcode %}

These have no relationship with the kernel directly.

{% hint style="info" %}
If you need to set the MOTD and MAL messages, you need to use the `SetMotd()` and `SetMal()` functions.
{% endhint %}

</details>

<details>

<summary>Moved <code>HostName</code> from Kernel to <code>NetworkTools</code></summary>

{% code title="Kernel.vb" lineNumbers="true" %}
```vb
Public HostName As String
```
{% endcode %}

It has no relationship with the kernel either.

{% hint style="info" %}
If you need to change the hostname, you need to use the `ChangeHostname` function in `NetworkTools`.

{% code title="NetworkTools.cs" lineNumbers="true" %}
```csharp
public static void ChangeHostname(string NewHost) { }
```
{% endcode %}
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 4 to Milestone 5</mark>

During Milestone 5's development, we have made the following breaking changes:

<details>

<summary>Renamed permissions to groups</summary>

{% code title="PermissionManagement.cs" lineNumbers="true" %}
```csharp
public static class PermissionManagement
```
{% endcode %}

We have renamed the permissions feature to `groups` to avoid confusion. Later, it's been renamed to user flags in later development versions.

</details>

***

## <mark style="color:$primary;">From Milestone 5 to Milestone 7</mark>

During Milestone 7's development, we have made the following breaking changes:

<details>

<summary>Made abstractions regarding the color management class</summary>

The color management used to define so many variables for just one color type. Now, it has been simplified to ease the making of the new color type. Color types are renamed to match all files that mention the color type.

As a result, we have removed all separate variables for each color type and merged them to simplify the declaration.

Also, we have added `GetColor()` and `SetColor()` functions to `ColorTools` to perform operations on these color types.

</details>

<details>

<summary>Moved <code>ConfigCategory</code> outside <code>Config</code> class</summary>

{% code title="Config.vb" lineNumbers="true" %}
```vb
Public Enum ConfigCategory
```
{% endcode %}

We have moved `ConfigCategory` outside the Config class to better organize the enumerations relating to the configuration.

</details>

<details>

<summary>Use <code>CommandArgumentInfo</code> in arguments</summary>

{% code title="ArgumentInfo.vb" lineNumbers="true" %}
```vb
Public Sub New(Argument As String, Type As ArgumentType, HelpDefinition As String, HelpUsage As String, ArgumentsRequired As Boolean, MinimumArguments As Integer, ArgumentBase As ArgumentExecutor, Optional Obsolete As Boolean = False, Optional AdditionalHelpAction As Action = Nothing)
```
{% endcode %}

Using `CommandArgumentInfo` allows you to define argument information for commands. However, it's a powerful class for managing arguments for commands and kernel arguments themselves.

As a result, we've used `CommandArgumentInfo` in `ArgumentInfo`.

{% hint style="info" %}
You need to change how you call the constructor of `ArgumentInfo` to hold the `CommandArgumentInfo` instance.

{% code title="ArgumentInfo.cs" lineNumbers="true" %}
```csharp
public ArgumentInfo(string Argument, string HelpDefinition, CommandArgumentInfo ArgArgumentInfo, ArgumentExecutor ArgumentBase, bool Obsolete = false, Action AdditionalHelpAction = null)
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Removed <code>SetColors</code> as they're no longer used</summary>

{% code title="ColorTools.vb" lineNumbers="true" %}
```vb
Public Function TrySetColors(InputColor As String, LicenseColor As String, ContKernelErrorColor As String, UncontKernelErrorColor As String, HostNameShellColor As String, UserNameShellColor As String,
                             BackgroundColor As String, NeutralTextColor As String, ListEntryColor As String, ListValueColor As String, StageColor As String, ErrorColor As String, WarningColor As String,
                             OptionColor As String, BannerColor As String, NotificationTitleColor As String, NotificationDescriptionColor As String, NotificationProgressColor As String,
                             NotificationFailureColor As String, QuestionColor As String, SuccessColor As String, UserDollarColor As String, TipColor As String, SeparatorTextColor As String,
                             SeparatorColor As String, ListTitleColor As String, DevelopmentWarningColor As String, StageTimeColor As String, ProgressColor As String, BackOptionColor As String,
                             LowPriorityBorderColor As String, MediumPriorityBorderColor As String, HighPriorityBorderColor As String, TableSeparatorColor As String, TableHeaderColor As String,
                             TableValueColor As String, SelectedOptionColor As String, AlternativeOptionColor As String) As Boolean
Public Sub SetColors(InputColor As String, LicenseColor As String, ContKernelErrorColor As String, UncontKernelErrorColor As String, HostNameShellColor As String, UserNameShellColor As String,
                     BackgroundColor As String, NeutralTextColor As String, ListEntryColor As String, ListValueColor As String, StageColor As String, ErrorColor As String, WarningColor As String,
                     OptionColor As String, BannerColor As String, NotificationTitleColor As String, NotificationDescriptionColor As String, NotificationProgressColor As String,
                     NotificationFailureColor As String, QuestionColor As String, SuccessColor As String, UserDollarColor As String, TipColor As String, SeparatorTextColor As String,
                     SeparatorColor As String, ListTitleColor As String, DevelopmentWarningColor As String, StageTimeColor As String, ProgressColor As String, BackOptionColor As String,
                     LowPriorityBorderColor As String, MediumPriorityBorderColor As String, HighPriorityBorderColor As String, TableSeparatorColor As String, TableHeaderColor As String,
                     TableValueColor As String, SelectedOptionColor As String, AlternativeOptionColor As String)
```
{% endcode %}

We have improved the color tools module, so SetColors is no longer used. We've removed it for this reason. Use `SetColor()` instead.

{% hint style="info" %}
To set the kernel type to a specified color, use `SetColor()`.

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static Color SetColor(KernelColorType type, Color color) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Changed algorithm enum to <code>EncryptionAlgorithms</code></summary>

{% code title="Encryption.vb" lineNumbers="true" %}
```vb
Public Enum Algorithms
```
{% endcode %}

As part of an ongoing change to the encryption driver, we've changed the algorithm enumeration to `EncryptionAlgorithms` outside the `Encryption` module.

{% hint style="info" %}
Encryption driver no longer uses the `EncryptionAlgorithms` enumeration, although it now handles custom algorithms. The enumeration can't be used anymore.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 7 to Milestone 8</mark>

During Milestone 8's development, we have made the following breaking changes:

<details>

<summary>Renamed two classes related to shell</summary>

{% code lineNumbers="true" %}
```vb
Public Class ShellInfo
Public MustInherit Class ShellExecutor
    Implements IShell
```
{% endcode %}

We have renamed the below two shell-related classes to the ones that suit the narrative of the classes.

{% hint style="info" %}
These classes can still be called using the following names:

* `ShellInfo` -> `ShellExecuteInfo`
* `ShellExecutor` -> `BaseShell`
{% endhint %}

</details>

<details>

<summary>Moved <code>TextLocation</code> to <code>Misc.Text</code></summary>

{% code title="TextLocation.vb" lineNumbers="true" %}
```vb
Public Enum TextLocation
```
{% endcode %}

This is a text-related enumeration of text vertical location (top, bottom). It's used by the splashes.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Misc` to `KS.Misc.Text`.
{% endhint %}

</details>

<details>

<summary>Moved <code>GetCommands</code> to <code>CommandManager</code></summary>

{% code title="GetCommand.vb" lineNumbers="true" %}
```vb
Public Function GetCommands(ShellType As ShellType) As Dictionary(Of String, CommandInfo)
```
{% endcode %}

This sub is more of a command management routine than the "getting command" module work itself.

{% hint style="info" %}
`GetCommands()` has been moved from `GetCommand` module to `CommandManager` module.
{% endhint %}

</details>

<details>

<summary>Changed the entire event system</summary>

{% code title="Events.vb" lineNumbers="true" %}
```vb
Public Class Events
```
{% endcode %}

{% code title="Kernel.vb" lineNumbers="true" %}
```vb
Public ReadOnly KernelEventManager As New Events
```
{% endcode %}

We have moved all the events to its own dedicated array containing all the available events that the kernel introduced, removing the giant Events class and its variable, `KernelEventManager`, in the Kernel entry point class. This will reduce the need of importing the Kernel namespace and class everytime we need to directly manage the events.

Event firing and response functions are moved to the EventsManager class in one function, `FireEvent`.

{% hint style="info" %}
To fire events, you now have to use the `FireEvent` function found under the `EventsManager` module. Its method signature is printed below:

{% code title="EventsManager.cs" lineNumbers="true" %}
```csharp
public static void FireEvent(EventType Event, params object[] Params) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Moved <code>NewLine</code> from <code>Kernel</code> to <code>CharManager</code></summary>

{% code title="Kernel.vb" lineNumbers="true" %}
```vb
Public ReadOnly NewLine As String
```
{% endcode %}

This is actually a character management function and not a function directly to the kernel.

{% hint style="info" %}
This variable is now found under `KS.Misc.Text.CharManager`.
{% endhint %}

</details>

<details>

<summary>Moved <code>KS.Login</code> to <code>KS.Users.Login</code></summary>

This has to do with the user management namespace, so we moved it to that namespace.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Login` to `KS.Users.Login`.
{% endhint %}

</details>

<details>

<summary>Moved <code>Kernel[Api]Version</code> to <code>KernelTools</code></summary>

{% code title="Kernel.vb" lineNumbers="true" %}
```vb
'From 0.0.24.0
Public ReadOnly KernelVersion As String
```
{% endcode %}

We didn't want the `Kernel` class to be publicly accessible, since it has been planned back at 0.0.1 as the class responsible for being an entry point. As a result, these variables, `KernelVersion` and `KernelApiVersion`, were successfully moved to `KernelTools`.

{% hint style="info" %}
To use these variables in their new location, change the reference from `Kernel` to `KernelTools`.
{% endhint %}

</details>

<details>

<summary>Removed <code>ColoredShell</code></summary>

{% code title="Shell.vb" lineNumbers="true" %}
```vb
Public ColoredShell As Boolean
```
{% endcode %}

The colors are now an essential part of KS, so we decided to take out support for uncolored shell.

</details>

<details>

<summary>Finally condensed <code>TableColor</code></summary>

{% code title="TableColor.vb" lineNumbers="true" %}
```vb
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, Color As ConsoleColor, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, ForegroundColor As ConsoleColor, BackgroundColor As ConsoleColor, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, ColTypes As ColTypes, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, colorTypeForeground As ColTypes, colorTypeBackground As ColTypes, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, Color As Color, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
Public Sub WriteTable(Headers() As String, Rows(,) As String, Margin As Integer, ForegroundColor As Color, BackgroundColor As Color, Optional SeparateRows As Boolean = True, Optional CellOptions As List(Of CellOptions) = Nothing)
```
{% endcode %}

We noticed that the code is repetitive for making tables, and we don't want to update six locations every bug fix, so we decided to condense it to a single code.

As a side-effect, we've changed the color signatures from foreground and background pairs to header, value, separator, and background colors. Consequently, we've removed the `ConsoleColor` version of `TableColor` as we found it irrelevant thanks to the enhanced `Color` class found in the Terminaux library.

{% hint style="info" %}
Use the new method signatures to write your table. As for the `ConsoleColor` version, we advice you to upgrade to `ConsoleColors` at minimum.

{% code title="TableColor.cs" lineNumbers="true" %}
```csharp
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, bool SeparateRows = true, List<CellOptions> CellOptions = null) { }
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, KernelColorType colorTypeSeparatorForeground, KernelColorType colorTypeHeaderForeground, KernelColorType colorTypeValueForeground, KernelColorType colorTypeBackground, bool SeparateRows = true, List<CellOptions> CellOptions = null) { }
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, ConsoleColors SeparatorForegroundColor, ConsoleColors HeaderForegroundColor, ConsoleColors ValueForegroundColor, ConsoleColors BackgroundColor, bool SeparateRows = true, List<CellOptions> CellOptions = null) { }
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, Color SeparatorForegroundColor, Color HeaderForegroundColor, Color ValueForegroundColor, Color BackgroundColor, bool SeparateRows = true, List<CellOptions> CellOptions = null) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Tried to balance color support for writers</summary>

Migration from `ConsoleColor` to `ConsoleColors` is complete. This means that all the writers in the `KS.Misc.*Writers` now have the `ConsoleColors` support.

The latest ColorSeq version, 1.0.2, will be used to make it easier to achieve.

{% hint style="info" %}
It's best to upgrade your `ConsoleColor` variables to `ConsoleColors` at minimum.
{% endhint %}

</details>

<details>

<summary>Added last argument support to auto completer</summary>

{% code title="CommandArgumentInfo.cs" lineNumbers="true" %}
```csharp
public Func<string[]> AutoCompleter { get; private set; }
```
{% endcode %}

We've added support for the last argument written to aid the auto completer in completing the command according to the last argument written. This is to ensure completions in the right context.

{% hint style="info" %}
If your command needs this feature, it's best to implement it.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone 8 to Milestone X</mark>

During Milestone X's development, we have made the following breaking changes:

<details>

<summary>Renamed command executor and base to reduce confusion</summary>

{% code lineNumbers="true" %}
```vb
Public Module GetCommand
Public MustInherit Class CommandExecutor
    Implements ICommand
```
{% endcode %}

Base command class had the name of `CommandExecutor`. However, it behaved like the base class for your mod commands, so we renamed it to `BaseCommand`. This caused us to rename the command execution class to `CommandExecutor`.

{% hint style="info" %}
To use the new names, you have to rename the following in this order:

* `CommandExecutor` -> `BaseCommand`
* `GetCommand` -> `CommandExecutor`
{% endhint %}

</details>

<details>

<summary>Renamed <code>ConsoleSanityChecker</code> to <code>ConsoleChecker</code></summary>

{% code title="ConsoleSanityChecker.vb" lineNumbers="true" %}
```vb
Public Module ConsoleSanityChecker
```
{% endcode %}

This class will be filled by many console checks, so renamed it according to the purpose.

{% hint style="info" %}
To use the methods inside the class, rename the references from `ConsoleSanityChecker` -> `ConsoleChecker`.
{% endhint %}

</details>

<details>

<summary><code>WriteWherePlain</code> from <code>TextWriterWhereColor</code> renamed</summary>

{% code title="TextWriterWhereColor.vb" lineNumbers="true" %}
```vb
Public Sub WriteWherePlain(msg As String, Left As Integer, Top As Integer, ParamArray vars() As Object)
Public Sub WriteWherePlain(msg As String, Left As Integer, Top As Integer, [Return] As Boolean, ParamArray vars() As Object)
```
{% endcode %}

This change is necessary to fit in with the rest of the `ConsoleWriters`

{% hint style="info" %}
To continue using the plain writer, rename the references from `WriteWherePlain` -> `WriteWhere`.
{% endhint %}

</details>

<details>

<summary>Removed <code>Screensaver.colors</code></summary>

{% code title="Screensaver.vb" lineNumbers="true" %}
```vb
Public ReadOnly colors() As ConsoleColor = CType([Enum].GetValues(GetType(ConsoleColor)), ConsoleColor())
Public ReadOnly colors255() As ConsoleColors = CType([Enum].GetValues(GetType(ConsoleColors)), ConsoleColors())
```
{% endcode %}

This is to remove support for 255 colors in screensavers.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

</details>

<details>

<summary>Moved <code>KS.Network</code> classes to <code>KS.Network.Base</code></summary>

{% code lineNumbers="true" %}
```vb
Public Module NetworkAdapter
Public Module NetworkAdapterPrint
Public Module NetworkTools
```
{% endcode %}

These classes are believed to be the base classes for the networking. These classes are used for general networking purposes.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Network` to `KS.Network.Base`.
{% endhint %}

</details>

<details>

<summary>Condensed speed dial to <code>KS.Network.SpeedDial</code></summary>

The speed dial API wasn't touched for a long time, so we decided to condense the speed dial API to a single namespace to ease the addition of the speed dial feature to all the networking shells.

In consequence, the speed dial format has changed.

{% code title="Old format" lineNumbers="true" %}
```json
  "ftp.riken.jp": {
    "Address": "ftp.riken.jp",
    "Port": 21,
    "User": "anonymous",
    "Type": 0,
    "FTP Encryption Mode": 0
  },
```
{% endcode %}

{% code title="New format" lineNumbers="true" %}
```json
  "ftp.us.debian.org": {
    "Address": "ftp.us.debian.org",
    "Port": 21,
    "Type": 0,
    "Options": [
      "anonymous",
      0
    ]
  }
```
{% endcode %}

The username and FTP encryption mode is now moved to Options, which is an array of options that the networking shells use. To convert your speed dial entries, you have to manually open all FTP and SFTP speed dial JSON files and make changes to transition from the old format to the new format.

</details>

<details>

<summary>Moved network transfer functions to <code>KS.Network.Base.Transfer</code></summary>

{% code lineNumbers="true" %}
```vb
Public Module NetworkTransfer
Public Class NetworkTransferInfo
Public Enum NetworkTransferType
```
{% endcode %}

We've done that to the base network classes, so why not do the same to the network transfer functions?

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Network.Transfer` to `KS.Network.Base.Transfer`.
{% endhint %}

</details>

<details>

<summary>Kernel exception handling changed</summary>

We have changed the way how the kernel exception handling works. We have simplified the code, merging all the exception classes to just one enumeration to help you filter kernel exceptions matching a specific exception.

This also helps us in making dynamic suggestions to specific error type in the future.

{% hint style="warning" %}
As a consequence, mods that use old handling now break, and should use this format to continue working as usual:

{% code lineNumbers="true" %}
```csharp
catch (KernelException ke) when (ke.ExceptionType == KernelExceptionType.ErrorType)
```
{% endcode %}

...where `ErrorType` is an error type obtained from the `KernelExceptionType` enumeration.
{% endhint %}

</details>

<details>

<summary>Changed <code>GetFilteredPositions</code> to tuple</summary>

{% code title="ConsoleExtensions.vb" lineNumbers="true" %}
```vb
Public Sub GetFilteredPositions(Text As String, ByRef Left As Integer, ByRef Top As Integer, ParamArray Vars() As Object)
```
{% endcode %}

To aid in simplicity of the function, we've replaced the two reference variables with the tuples in their respective orders of cursor left and top positions.

{% hint style="info" %}
The first tuple value in the returned value specifies the filtered X position, and the second one specifies the filtered Y position in the console buffer.

{% code title="ConsoleExtensions.cs" lineNumbers="true" %}
```csharp
public static (int, int) GetFilteredPositions(string Text, params object[] Vars) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Internalized several kernel tools</summary>

{% code title="KernelTools.vb" lineNumbers="true" %}
```vb
Public Sub KernelError(ErrorType As KernelErrorLevel, Reboot As Boolean, RebootTime As Long, Description As String, Exc As Exception, ParamArray Variables() As Object)
Sub GeneratePanicDump(Description As String, ErrorType As KernelErrorLevel, Exc As Exception)
Sub ResetEverything()
Sub InitEverything(Args() As String)
Sub FactoryReset()
Sub ReportNewStage(StageNumber As Integer, StageText As String)
```
{% endcode %}

These tools could be abused, so we decided to privatize these tools.

{% hint style="danger" %}
We advice you to cease using these functions.
{% endhint %}

</details>

<details>

<summary>Removed <code>PrepareDict</code></summary>

{% code title="Translate.vb" lineNumbers="true" %}
```vb
Public Function PrepareDict(lang As String) As Dictionary(Of String, String)
```
{% endcode %}

`PrepareDict` used to populate the string dictionary with definitions to the localized string. Now, because the language management routine was remodeled, we've removed `PrepareDict` as part of the change.

{% hint style="danger" %}
The language manager automatically does this each time your mod sets the language, so we advice you to cease using this function.
{% endhint %}

</details>

<details>

<summary>Removed network adapter querying</summary>

{% code lineNumbers="true" %}
```vb
'NetworkAdapter.vb
Public Function IsInternetAdapter(InternetAdapter As NetworkInterface) As Boolean

'NetworkAdapterPrint.vb
Public Sub PrintAdapterProperties()
Sub PrintAdapterIPv4Info(NInterface As NetworkInterface, Properties As IPv4InterfaceProperties, Statistics As IPv4InterfaceStatistics, AdapterNumber As Long)
Sub PrintAdapterIPv6Info(NInterface As NetworkInterface, Properties As IPv6InterfaceProperties, AdapterNumber As Long)
Sub PrintGeneralNetInfo(IPv4Stat As IPGlobalStatistics, IPv6Stat As IPGlobalStatistics)
```
{% endcode %}

The network adapter querying functionality was implemented in 0.0.3. This functionality was no longer maintained as it wasn't tweaked.

{% hint style="danger" %}
We advice you to cease using this functionality.
{% endhint %}

</details>

<details>

<summary>Theme preview is no longer exclusive to theme studio</summary>

{% code title="ThemeStudioTools.vb" lineNumbers="true" %}
```vb
Sub PreparePreview()
```
{% endcode %}

The theme preview routine used to depend on the theme studio to do its job, under the name of `ThemeStudioTools.PreparePreview()`. However, because there were recent improvements to the theming system, we've finally condensed the preview routine to `ThemeTools.PreviewTheme()`.

You can no longer use the old method, because it also required loading the theme information to the theme studio itself. What if it was called in a context that has no relationship with the theme studio, such as in the case of `themesel`?

{% hint style="info" %}
You can use the new `ThemeTools.PreviewTheme()` function to preview any theme. The method signatures are written below.

{% code title="ThemeTools.cs" lineNumbers="true" %}
```csharp
public static void PreviewTheme(string theme) { }
public static void PreviewTheme(ThemeInfo theme) { }
public static void PreviewTheme(Dictionary<KernelColorType, Color> colors) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Migrated kernel arguments</summary>

{% code lineNumbers="true" %}
```vb
Public Enum ArgumentType
Public Module CommandLineArgs
Public Module ArgumentPrompt
```
{% endcode %}

We used to provide two argument channels: one for the command-line kernel arguments, and one for the kernel arguments. The entry point has been provided the `Args` variable to get all the arguments from the command line. Since it has undergone recent improvements to the system, we've decided to remove the kernel arguments channel, so we don't have to parse the passed arguments twice.

We also had to remove the `arginj` command, one of the commands that made appearance in first-generation versions of KS.

</details>

<details>

<summary>Removed <code>GetCompilerVars</code></summary>

{% code title="KernelTools.vb" lineNumbers="true" %}
```vb
Public Function GetCompilerVars() As String()
```
{% endcode %}

This was only useful in conditions where getting the compiler variables for determining the kernel milestone is needed, which was seldom needed by mods. We've removed it.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

</details>

<details>

<summary>Migrated encryptors to Kernel Drivers</summary>

The kernel drivers are beneficial, so we decided to give the encryptors a chance to appear in kernel drivers. This caused us to remove `EncryptionAlgorithms` and `IEncryptor` and replace them with `IEncryptionDriver`, handled by the kernel driver handler.

{% hint style="info" %}
You can implement your own encryptor by registering your custom encryption driver using the `RegisterDriver` function.

{% code title="DriverHandler.cs" lineNumbers="true" %}
```csharp
public static void RegisterDriver(DriverTypes type, IDriver driver) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Removed <code>TwoNewlines</code> argument from <code>WriteLicense</code></summary>

{% code title="WelcomeMessage.vb" lineNumbers="true" %}
```vb
Sub WriteLicense(TwoNewlines As Boolean)
```
{% endcode %}

This argument was unused, so we decided to remove it from `WriteLicense()`.

{% hint style="danger" %}
We advice you to cease using this variable.
{% endhint %}

</details>

<details>

<summary>Renamed <code>PartInfo</code> to <code>ModPartInfo</code></summary>

{% code title="PartInfo.vb" lineNumbers="true" %}
```vb
Public Class PartInfo
```
{% endcode %}

Add `Mod` next to `PartInfo` to clarify which module uses this.

{% hint style="info" %}
To implement your new mod parts, construct the `ModPartInfo` class. For existing mod parts, rename `PartInfo` to `ModPartInfo`.
{% endhint %}

</details>

<details>

<summary>Manual pages moved to <code>Modifications</code></summary>

{% code lineNumbers="true" %}
```vb
Public Class Manual
Public Module PageManager
Module PageParser
Public Module PageViewer
```
{% endcode %}

These manual pages are used by mods to host documentation, so we moved it to `KS.Modifications.ManPages` to reflect its purpose.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.ManPages` to `KS.Modifications.ManPages`.
{% endhint %}

</details>

<details>

<summary>Changed <code>Notifications</code> to <code>NotificationManager</code></summary>

{% code title="Notifications.vb" lineNumbers="true" %}
```vb
Public Module Notifications
```
{% endcode %}

We felt that both the `Notification` and `Notifications` classes are confusing for some people, so we decided to make these clearer by renaming the `Notifications` class to `NotificationManager`

{% hint style="info" %}
To use the methods inside the class, rename the references from `Notifications` -> `NotificationManager`.
{% endhint %}

</details>

<details>

<summary>Removed getting property value in variable</summary>

{% code title="PropertyManager.vb" lineNumbers="true" %}
```vb
Public Function GetPropertyValueInVariable(Variable As String, [Property] As String) As Object
Public Function GetPropertyValueInVariable(Variable As String, [Property] As String, VariableType As Type) As Object
```
{% endcode %}

`VariableProperty` is no longer used, so we decided to remove it. As a consequence, we also had to remove the `PropertyManager.GetPropertyValueInVariable()` routine.

{% hint style="danger" %}
We advise you to cease using these functions.
{% endhint %}

</details>

***

## <mark style="color:$primary;">From Milestone X to Beta 1</mark>

During Beta 1's development, we have made the following breaking changes:

<details>

<summary>Moved <code>ColTypes</code> to <code>KernelColorType</code></summary>

{% code title="ColorTools.vb" lineNumbers="true" %}
```vb
Public Enum ColTypes As Integer
```
{% endcode %}

This is an enumeration which simply tells the difference of all the defined and known kernel color types. We have moved ColTypes to KernelColorType.

{% hint style="info" %}
To continue using the kernel color type enumeration, rename the references from `ColTypes` to `KernelColorType`, importing the `KS.ConsoleBase.Colors` namespace.

{% code title="KernelColorType.cs" lineNumbers="true" %}
```csharp
public enum KernelColorType { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Removed <code>ref</code> from conditional debug writers</summary>

{% code title="DebugWriter.vb" lineNumbers="true" %}
```vb
Public Sub WdbgConditional(ByRef Condition As Boolean, Level As DebugLevel, text As String, ParamArray vars() As Object)
Public Sub WStkTrcConditional(ByRef Condition As Boolean, Ex As Exception)
```
{% endcode %}

The conditional debug writers didn't do anything to the boolean condition that caused it to change its state, so we decided to pass the boolean value by value and not by reference.

{% hint style="info" %}
Remove the `ref` prefix from the boolean variable that is being tested from your conditional debug writer calls. Follow the below method signatures:

{% code title="DebugWriters.cs" lineNumbers="true" %}
```csharp
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object[] vars) { }
public static void WriteDebugStackTraceConditional(bool Condition, Exception Ex) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Removed <code>GroupManagement</code> (a.k.a. <code>PermissionManagement</code>)</summary>

{% code title="PermissionManagement.vb" lineNumbers="true" %}
```vb
Public Module PermissionManagement
```
{% endcode %}

The `GroupManagement` module was removed in preparation for the new permission system. The groups were moved outside in the users JSON file to become singular boolean variables, and the permission system was implemented under the `KS.Users.Permissions` namespace.

{% hint style="info" %}
To grant or revoke individual permissions from a specified user, use the following functions:

* `GrantPermission`
* `RevokePermission`

You may need to import the `KS.Users.Permissions` namespace to use this feature, although it works on all permissions, unlike the superuser variable which grants all permissions.

Their method signatures are written below.

{% code title="PermissionsTools.cs" lineNumbers="true" %}
```csharp
public static void GrantPermission(string User, PermissionTypes permissionType) { }
public static void RevokePermission(string User, PermissionTypes permissionType) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Removed obsolete functions</summary>

{% code lineNumbers="true" %}
```vb
'Input.vb
Public Function ReadLineUntil(ByRef Condition As Boolean) As String

'ThreadManager.vb
Public Sub SleepNoBlock(Time As Long, ThreadWork As BackgroundWorker)

'NetworkTools.vb
Public Sub ConvertSpeedDialEntries(SpeedDialType As SpeedDialType)
```
{% endcode %}

`ReadLineUntil()`, `SleepNoBlock()`, and `ConvertSpeedDialEntries()` were removed for being obsolete.

The first function was removed in favor of ReadLine.Reboot and TermRead, the second function was removed for the absence of our usage of `BackgroundWorker`, and the third function was removed as a result of huge improvements to the speed dial functionality that makes it incompatible with the older speed dial format.

{% hint style="danger" %}
We advice you to cease using these functions.
{% endhint %}

{% hint style="warning" %}
To sleep without blocking, convert all your `BackgroundWorker`s to `KernelThread` and use the appropriate `SleepNoBlock` overload for your kernel thread. The below method signature is shown.

{% code title="ThreadManager.cs" lineNumbers="true" %}
```csharp
public static void SleepNoBlock(long Time, KernelThread ThreadWork) { }
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Argument auto-completion re-implemented</summary>

{% code title="CommandArgumentInfo.vb" lineNumbers="true" %}
```vb
Public Sub New(HelpUsages() As String, ArgumentsRequired As Boolean, MinimumArguments As Integer, Optional AutoCompleter As Func(Of String()) = Nothing)
```
{% endcode %}

Command auto-completion used to be available on ReadLine.Reboot to automatically complete the command needed to run. However, ReadLine.Reboot has come to an end, so we decided to re-implement it to align with TermRead.

As a result, the auto completion facility in your shell, if it has one implemented in your `CommandArgumentInfo`, will have to be re-implemented to parse the whole command passed to the auto-completion builder, `AutoCompleter`, and generate suggestions based on that data.

{% hint style="info" %}
In your `CommandInfo` implementation of your command, you'll also have to re-implement it so that the auto-completer takes three arguments. You can always discard the index and delimiters argument in your action declaration: `(Text, _, _) => Function(Text)`.

{% code title="CommandArgumentInfo.cs" lineNumbers="true" %}
```csharp
public CommandArgumentInfo(string[] Arguments, SwitchInfo[] Switches, bool ArgumentsRequired, int MinimumArguments, bool AcceptsSet = false, Func<string, int, char[], string[]> AutoCompleter = null)
```
{% endcode %}
{% endhint %}

</details>

<details>

<summary>Converted kernel exceptions</summary>

Previously, we've used the built-in .NET exceptions to catch appropriate exceptions based on the context of an error. Since `KernelException` was implemented as part of the first development semester of Nitrocid KS 0.1.0, we decided to throw all the exceptions to `KernelException` that dynamically provides extended information as to what's wrong, coupled together with possible suggestions and extra messages.

{% hint style="info" %}
In order to throw these exceptions, you must now route all your exception handlers in your mods to target `KernelException` and check the exception type before you can take action. Converted exceptions are found in [this commit](https://github.com/Aptivi/Kernel-Simulator/commit/1d4d31cd12087659b807687d286047013a22273b).
{% endhint %}

</details>

<details>

<summary>Removed decisive writers</summary>

{% code title="Decisive.vb" lineNumbers="true" %}
```vb
Public Sub DecisiveWrite(CommandType As ShellType, DebugDeviceSocket As StreamWriter, Text As String, Line As Boolean, colorType As ColTypes, ParamArray vars() As Object)
```
{% endcode %}

We used to implement the decisive writers to decide whether to use the normal console writer or to use the remote debug connection according to the shell type. Over time, the remote debug shell was removed and later implemented as a standalone add-on for the remote debugger. This leads to us removing this decisive writer from the `MiscWriters` namespace.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

</details>

<details>

<summary>Moved <code>PlaceParse</code> to <code>KS.Misc.Probers.Placeholder</code></summary>

{% code title="PlaceParse.vb" lineNumbers="true" %}
```vb
Public Module PlaceParse
```
{% endcode %}

This module used to statically replace all the text placeholders found within the text with their values. It used to exist in the `KS.Misc.Probers` namespace, but we moved it to the `KS.Misc.Probers.Placeholder` namespace to align with the latest Nitrocid KS API design. It also earned a new way to dynamically parse the placeholders.

{% hint style="info" %}
The function names and the module itself are unchanged, but we just need you to change the namespace import to the abovementioned namespace.
{% endhint %}

</details>

<details>

<summary>Removed <code>KernelColorType.Gray</code></summary>

{% code title="ColorTools.vb" lineNumbers="true" %}
```vb
''' <summary>
''' Gray color (for special purposes)
''' </summary>
Gray
```
{% endcode %}

This color type was used as a special color type intended to indicate that the element highlighted is colorless. Since we already have `ColorTools.GetGray()` to get the gray color according to the background color, and since this color type is just a wrapper to this function, we decided to remove this kernel color type.

{% hint style="info" %}
Instead of using `KernelColorType.Gray`, use the `ColorTools.GetGray()` function to get the gray color.
{% endhint %}

</details>

<details>

<summary>Replaced <code>GetVariables()</code> with <code>Variables</code> property</summary>

{% code title="UESHVariables.vb" lineNumbers="true" %}
```vb
Public Function GetVariables() As Dictionary(Of String, String)
```
{% endcode %}

This function used to return a list of available UESH variables. It's been replaced with a property that does exactly the same thing. It's to make your mod code related to UESH variables easier to read.

{% hint style="info" %}
Replace all calls to `UESHVariables.GetVariables()` with `Variables`.
{% endhint %}

</details>

<details>

<summary>Removed remote-debug-related argument from <code>ShowHelp()</code></summary>

{% code title="HelpSystem.vb" lineNumbers="true" %}
```vb
Public Sub ShowHelp(command As String, CommandType As ShellType, Optional DebugDeviceSocket As StreamWriter = Nothing)
                                                                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
{% endcode %}

Remote debug shell used to require the `DebugDeviceSocket` parameter to be passed to `ShowHelp` for `DecisiveWriter` to decide what type of console is going to be written to. Since `DecisiveWriter` got removed and the remote debug shell was re-implemented to be standalone, we decided to remove this parameter.

{% hint style="info" %}
There was no need to pass `DebugDeviceSocket` to this function anyways. If you really need to use it, make your own remote debug command with the help entry, and Nitrocid KS will take care of the rest.
{% endhint %}

</details>

<details>

<summary>Renamed few classes</summary>

{% code title="TimeDate.vb" lineNumbers="true" %}
```vb
Namespace TimeDate
    Public Module TimeDate
```
{% endcode %}

{% code title="IScript.vb" lineNumbers="true" %}
```vb
Namespace Modifications
    Public Interface IScript
```
{% endcode %}

`TimeDate` used to host all the time and date general properties and functions. However, its access required to reference the namespace and then the class, because both the namespace and the class have the same name. As a result, the `TimeDate` class is renamed to `TimeDateTools` for easier access.

Also, `IScript` used to be the heart of the kernel modifications. It's renamed to `IMod` since it doesn't have to do with the UESH scripts.

{% hint style="warning" %}
Your mods should change the implementation interface name of the mod, `IScript`, to the new name, `IMod`, as it's more fitting. This will break all mods.

For the time and date functions, use the new class name, `TimeDateTools`.
{% endhint %}

{% hint style="info" %}
None of the methods and properties on the two above classes are changed.
{% endhint %}

</details>
