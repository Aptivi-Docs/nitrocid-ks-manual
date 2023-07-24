---
description: Follow the compatibility notes when upgrading your mods to API v3.0
---

# 🔼 Upgrading to API v3.0

As API v3.0 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

{% hint style="danger" %}
.NET Framework 4.8 is **no longer supported** as of 0.1.0 Beta 1. Please consider using .NET 6.0 instead to continue using Nitrocid KS. This is to improve multi-platform support without having to go to one environment (`dotnetfx` on Windows and `mono` on Linux and macOS) for each platform.
{% endhint %}

### To 0.1.0

This version is a futuristic magic that brings in many feature additions and spectacular improvements in all fields, including cosmetic changes.

{% content-ref url="../version-release-notes/v0.1.x.x-series/" %}
[v0.1.x.x-series](../version-release-notes/v0.1.x.x-series/)
{% endcontent-ref %}

**Moved events to KS.Kernel.Events**

{% code title="Events.vb" lineNumbers="true" %}
```visual-basic
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
```visual-basic
Public Function ListAllFiredEvents() As Dictionary(Of String, Object())
Public Function ListAllFiredEvents(SearchTerm As String) As Dictionary(Of String, Object())
Public Sub ClearAllFiredEvents()
```
{% endcode %}

All of the event-related code files are moved to `KS.Kernel.Events` to separate these from the actual kernel code. However, because events are part of the kernel, we prefer to put it on `KS.Kernel` namespace rather than `KS.Misc`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel events from `KS.Misc` to `KS.Kernel.Events`.
{% endhint %}

**Moved PlatformDetector to KS.Kernel.KernelPlatform**

{% code title="PlatformDetector.vb" lineNumbers="true" %}
```visual-basic
Public Module PlatformDetector
```
{% endcode %}

It has come to the conclusion that `PlatformDetector` is now promoted to the Kernel namespace under the name `KernelPlatform` so you can access it under the `KS.Kernel` namespace.

{% hint style="info" %}
Change the namespace declaration to refer to kernel platform code from `KS.Misc` to `KS.Kernel.KernelPlatform`.
{% endhint %}

**Separated the MOTD and MAL parsers**

{% code title="MOTDParse.vb" lineNumbers="true" %}
```visual-basic
Public Enum MessageType As Integer
```
{% endcode %}

MOTD and MAL parsers were unified since early versions of Nitrocid KS. However, it didn't occur to us that we need to separate them for a very long time. We took actions to separate them, effectively removing the `MessageType` enumeration.

{% hint style="info" %}
* If you want to use the MOTD parser, use the `KS.Misc.Probers.Motd` namespace to use the `MotdParse` static class methods.
* However, if you want to use the MAL parser, use the `KS.Misc.Probers.Mal` namespace to use the `MalParse` static class methods.
{% endhint %}

**Moved GetTerminal\* to KernelPlatform**

{% code title="ConsoleExtensions.vb" lineNumbers="true" %}
```visual-basic
Public Function GetTerminalEmulator() As String
Public Function GetTerminalType() As String
```
{% endcode %}

These two functions are actually part of the terminal, and they make use of the `$TERM_PROGRAM` and `$TERM` environment variables, which are dependent on the terminal.

Since these usually are undefined in Windows, we put these functions to `KernelPlatform` to accomodate the change as platform-dependent, but we don't actually check for Linux to execute these functions, because some terminal emulators in Windows actually define these variables.

{% hint style="info" %}
Change the namespace declaration to refer to kernel terminal detection code from `KS.ConsoleBase` to `KS.Kernel.KernelPlatform`.
{% endhint %}

**Moved shell common folders to KS.Shell.Shells**

This is to separate the shell code for each tool from their folders to a unified namespace, `KS.Shell.Shells`. It houses every shell for every tool. This is to make creation of built-in shells easier.

{% hint style="info" %}
This means that `*ShellCommon` modules are moved to `KS.Shell.Shells.*` and every call to that module should be redirected to that namespace. The tools, however, stays intact.
{% endhint %}

**Removed MakePermanent()**

{% code title="ColorTools.vb" lineNumbers="true" %}
```visual-basic
Public Sub MakePermanent()
```
{% endcode %}

MakePermanent used to save all the colors to kernel configuration. This function was now removed as a result of recent configuration improvements.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

**Graduated `Configuration` to `KS.Kernel`**

{% code title="Config.vb" lineNumbers="true" %}
```visual-basic
Namespace Misc.Configuration
```
{% endcode %}

This configuration logic was smart enough to be graduated, since it's the core function in the kernel. It's used everywhere, including the `settings` command, which is an application that lets you adjust settings on the go.

**Graduated `FindSetting` and `CheckSettingsVariables`**

{% code title="SettingsApp.vb" lineNumbers="true" %}
```visual-basic
Public Function FindSetting(Pattern As String, SettingsToken As JToken) As List(Of String)
Public Function CheckSettingsVariables() As Dictionary(Of String, Boolean)
```
{% endcode %}

These two functions were unrelated to the settings app, but `FindSetting()` was what `KS.Misc.Settings.SettingsApp` uses, and `CheckSettingsVariables()` was renamed to `CheckConfigVariables()` to accommodate with the graduation.

{% hint style="info" %}
You can find these methods in the `ConfigTools` module located in the `KS.Kernel.Configuration` namespace.
{% endhint %}

{% code title="ConfigTools.cs" lineNumbers="true" %}
```csharp
public static List<InputChoiceInfo> FindSetting(string Pattern, JToken SettingsToken)
public static Dictionary<string, bool> CheckConfigVariables()
```
{% endcode %}

**Moved power management functions to `KS.Kernel.Power`**

These power management functions were there in `KernelTools` since the earliest version of KS. Now, they're relocated to `KS.Kernel.Power`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel power code from `KS.Kernel.KernelTools` to `KS.Kernel.Power`.
{% endhint %}

**Removed `InitPaths` in favor of properties**

{% code title="Paths.vb" lineNumbers="true" %}
```visual-basic
Sub InitPaths()
```
{% endcode %}

Now, we don't have to initialize paths every time we make an internal app that depends on Nitrocid KS's paths. The call to the function that gets the path, `GetKernelPath`, however won't be removed because it's widely used and is unaffected.

{% hint style="info" %}
This function is not part of the public API. Reflection calls to this function will stop working. We advice you to use the `GetKernelPath` function since it's much faster.
{% endhint %}

{% code title="Paths.cs" lineNumbers="true" %}
```csharp
public static string GetKernelPath(KernelPathType PathType)
```
{% endcode %}

**Moved kernel update code to `Kernel.Updates`**

These power management functions were there in `KernelTools` since the earliest version of KS. Now, they're relocated to `KS.Kernel.Updates`.

{% hint style="info" %}
Change the namespace declaration to refer to kernel update code from `KS.Kernel.KernelTools` to `KS.Kernel.Updates`.
{% endhint %}

**Removed `ListArgs` from `ICommand` and `IArgument`**

{% code lineNumbers="true" %}
```visual-basic
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

**Moved `GetEsc()` to `Misc.Text.CharManager`**

{% code title="Color255.vb" lineNumbers="true" %}
```visual-basic
Public Function GetEsc() As Char
```
{% endcode %}

`GetEsc()` is now widely used for color manipulation, but we need to move it to a better place as migration to `ColorSeq` is done.

{% code title="Color255.vb" lineNumbers="true" %}
```visual-basic
Public Module Color255
```
{% endcode %}

We have deleted `Color255` from `KS.ConsoleBase` as a result of this migration.

{% hint style="info" %}
Change the namespace declaration to refer to `GetEsc()` from `KS.ConsoleBase.Colors` to `KS.Misc.Text.CharManager`.
{% endhint %}

**Removed FullArgumentList**

{% code title="ProvidedCommandArgumentsInfo.vb" lineNumbers="true" %}
```visual-basic
Public ReadOnly Property FullArgumentsList As String()
```
{% endcode %}

Following the removal of `ListArgs()`, we can safely remove this property.

{% hint style="info" %}
Recent changes to the shell command parsing code have allowed reliable argument and switch parsing. Use the `ListArgsOnly` and `ListSwitchesOnly` arrays to process arguments and switches.
{% endhint %}

**Removed `ConsoleWriters.*.Write*Plain` in favor of the plain writers**

The plain writer interfaces feel like they're a great addition to control the console writers.

{% hint style="info" %}
Use the plain writers to replace the removed plain writers from the `ConsoleWriters`.
{% endhint %}

**Updated debug and notifications namespaces**

We felt that moving debug-related functions to `KS.Kernel` would be more convenient, so we moved these functions to it. Also, we've renamed the notifications namespace.

{% hint style="info" %}
The below namespaces were affected in this change:

* `KS.Misc.Writers.DebugWriters` -> `KS.Debugging`
* `KS.Network.RemoteDebug` -> `KS.Debugging.RemoteDebug`
* `KS.Misc.Notifiers` -> `KS.Misc.Notifications`
{% endhint %}

**Merged `ParseCmd` with `ExecuteCommand`**

{% code title="RemoteDebugCmd.vb" lineNumbers="true" %}
```visual-basic
Sub ParseCmd(CmdString As String, SocketStreamWriter As StreamWriter, Address As String)
```
{% endcode %}

It has come to the conclusion that `ParseCmd` is now very similar to `ExecuteCommand` with treating the remote debug shell specially. This is no longer needed as `ProvidedCommandArgumentsInfo` has been provided the IP address of the target device, making `ParseCmd` redundant.

{% hint style="info" %}
This function wasn't part of the public KS API. We advice you to cease using this function and start declaring your remote debug command.
{% endhint %}

**Removed `ExecuteRDAlias()`**

{% code title="AliasExecutor.vb" lineNumbers="true" %}
```visual-basic
Sub ExecuteRDAlias(aliascmd As String, SocketStream As IO.StreamWriter, Address As String)
```
{% endcode %}

This function was not needed to execute aliases since there has been recent improvements to the executor in both 0.0.20.0 and 0.0.24.0.

{% hint style="info" %}
This function wasn't part of the public KS API. We advice you to cease using this function.
{% endhint %}

**Renamed debug writer function names**

{% code title="DebugWriter.vb" lineNumbers="true" %}
```visual-basic
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
{% endhint %}

{% code title="DebugWriter.cs" lineNumbers="true" %}
```csharp
public static void WriteDebug(DebugLevel Level, string text, params object[] vars)
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object[] vars)
public static void WriteDebugDevicesOnly(DebugLevel Level, string text, params object[] vars)
public static void WriteDebugStackTraceConditional(bool Condition, Exception Ex)
public static void WriteDebugStackTrace(Exception Ex)
```
{% endcode %}

**Moved MAL and MOTD message to `Misc.Probers.Motd`**

{% code title="Kernel.vb" lineNumbers="true" %}
```visual-basic
Public MOTDMessage, MAL As String
```
{% endcode %}

These have no relationship with the kernel directly.

{% hint style="info" %}
If you need to set the MOTD and MAL messages, you need to use the `SetMotd` and `SetMal` functions.
{% endhint %}

{% code lineNumbers="true" %}
```csharp
public static void SetMotd(string Message)
public static void SetMal(string Message)
```
{% endcode %}

**Moved HostName from Kernel to NetworkTools**

{% code title="Kernel.vb" lineNumbers="true" %}
```visual-basic
Public HostName As String
```
{% endcode %}

It has no relationship with the kernel either.

{% hint style="info" %}
If you need to change the hostname, you need to use the `ChangeHostname` function in `NetworkTools`.
{% endhint %}

{% code title="NetworkTools.cs" lineNumbers="true" %}
```csharp
public static void ChangeHostname(string NewHost)
```
{% endcode %}

**Made abstractions regarding the color management class**

The color management used to define so many variables for just one color type. Now, it has been simplified to ease the making of the new color type. Color types are renamed to match all files that mention the color type.

As a result, we have removed all separate variables for each color type and merged them to simplify the declaration.

Also, we have added `GetColor()` and `SetColor()` functions to ColorTools to perform operations on these color types.

**Moved ConfigCategory outside Config class**

{% code title="Config.vb" lineNumbers="true" %}
```visual-basic
Public Enum ConfigCategory
```
{% endcode %}

We have moved ConfigCategory outside the Config class to better organize the enumerations relating to the configuration.

**Use CommandArgumentInfo in arguments**

{% code title="ArgumentInfo.vb" lineNumbers="true" %}
```visual-basic
Public Sub New(Argument As String, Type As ArgumentType, HelpDefinition As String, HelpUsage As String, ArgumentsRequired As Boolean, MinimumArguments As Integer, ArgumentBase As ArgumentExecutor, Optional Obsolete As Boolean = False, Optional AdditionalHelpAction As Action = Nothing)
```
{% endcode %}

Using `CommandArgumentInfo` allows you to define argument information for commands. However, it's a powerful class for managing arguments for commands and kernel arguments themselves.

As a result, we've used `CommandArgumentInfo` in `ArgumentInfo`.

{% hint style="info" %}
You need to change how you call the constructor of ArgumentInfo to hold the CommandArgumentInfo instance.
{% endhint %}

{% code title="ArgumentInfo.cs" lineNumbers="true" %}
```csharp
public ArgumentInfo(string Argument, string HelpDefinition, CommandArgumentInfo ArgArgumentInfo, ArgumentExecutor ArgumentBase, bool Obsolete = false, Action AdditionalHelpAction = null)
```
{% endcode %}

**Removed SetColors as they're no longer used**

{% code title="ColorTools.vb" lineNumbers="true" %}
```visual-basic
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
{% endhint %}

{% code title="ColorTools.cs" lineNumbers="true" %}
```csharp
public static Color SetColor(KernelColorType type, Color color)
```
{% endcode %}

**Changed algorithm enum to EncryptionAlgorithms**

{% code title="Encryption.vb" lineNumbers="true" %}
```visual-basic
Public Enum Algorithms
```
{% endcode %}

As part of an ongoing change to the encryption driver, we've changed the algorithm enumeration to `EncryptionAlgorithms` outside the `Encryption` module.

{% hint style="info" %}
Encryption driver no longer uses the `EncryptionAlgorithms` enumeration, although it now handles custom algorithms. The enumeration can't be used anymore.
{% endhint %}

**Renamed two classes related to shell**

{% code lineNumbers="true" %}
```visual-basic
Public Class ShellInfo
Public MustInherit Class ShellExecutor
    Implements IShell
```
{% endcode %}

We have renamed the below two shell-related classes to the ones that suit the narrative of the classes.

{% hint style="info" %}
These classes can still be called using the following names:

* ShellInfo -> ShellExecuteInfo
* ShellExecutor -> BaseShell
{% endhint %}

**Moved TextLocation to Misc.Text**

{% code title="TextLocation.vb" lineNumbers="true" %}
```visual-basic
Public Enum TextLocation
```
{% endcode %}

This is a text-related enumeration of text vertical location (top, bottom). It's used by the splashes.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Misc` to `KS.Misc.Text`.
{% endhint %}

**Moved GetCommands to CommandManager**

{% code title="GetCommand.vb" lineNumbers="true" %}
```visual-basic
Public Function GetCommands(ShellType As ShellType) As Dictionary(Of String, CommandInfo)
```
{% endcode %}

This sub is more of a command management routine than the "getting command" module work itself.

{% hint style="info" %}
`GetCommands()` has been moved from `GetCommand` module to `CommandManager` module.
{% endhint %}

**Changed the entire event system**

{% code title="Events.vb" lineNumbers="true" %}
```visual-basic
Public Class Events
```
{% endcode %}

{% code title="Kernel.vb" lineNumbers="true" %}
```visual-basic
Public ReadOnly KernelEventManager As New Events
```
{% endcode %}

We have moved all the events to its own dedicated array containing all the available events that the kernel introduced, removing the giant Events class and its variable, `KernelEventManager`, in the Kernel entry point class. This will reduce the need of importing the Kernel namespace and class everytime we need to directly manage the events.

Event firing and response functions are moved to the EventsManager class in one function, `FireEvent`.

{% hint style="info" %}
To fire events, you now have to use the FireEvent function found under the EventsManager module. Its method signature is printed below:
{% endhint %}

{% code title="EventsManager.cs" lineNumbers="true" %}
```csharp
public static void FireEvent(EventType Event, params object[] Params)
```
{% endcode %}

**Moved NewLine from Kernel to CharManager**

{% code title="Kernel.vb" lineNumbers="true" %}
```visual-basic
Public ReadOnly NewLine As String
```
{% endcode %}

This is actually a character management function and not a function directly to the kernel.

{% hint style="info" %}
This variable is now found under `KS.Misc.Text.CharManager`.
{% endhint %}

**Moved KS.Login to KS.Users.Login**

This has to do with the user management namespace, so we moved it to that namespace.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Login` to `KS.Users.Login`.
{% endhint %}

**Moved Kernel\[Api]Version to KernelTools**

{% code title="Kernel.vb" lineNumbers="true" %}
```visual-basic
'From 0.0.24.0
Public ReadOnly KernelVersion As String
```
{% endcode %}

We didn't want the `Kernel` class to be publicly accessible, since it has been planned back at 0.0.1 as the class responsible for being an entry point. As a result, these variables, `KernelVersion` and `KernelApiVersion`, were successfully moved to `KernelTools`.

{% hint style="info" %}
To use these variables in their new location, change the reference from `Kernel` to `KernelTools`.
{% endhint %}

**Removed `ColoredShell`**

{% code title="Shell.vb" lineNumbers="true" %}
```visual-basic
Public ColoredShell As Boolean
```
{% endcode %}

The colors are now an essential part of KS, so we decided to take out support for uncolored shell.

**Finally condensed `TableColor`**

{% code title="TableColor.vb" lineNumbers="true" %}
```visual-basic
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

As a side-effect, we've changed the color signatures from foreground and background pairs to header, value, separator, and background colors. Consequently, we've removed the `ConsoleColor` version of `TableColor` as we found it irrelevant thanks to the enhanced `Color` class found in the ColorSeq library.

{% hint style="info" %}
Use the new method signatures to write your table. As for the ConsoleColor version, we advice you to upgrade to ConsoleColors at minimum.
{% endhint %}

{% code title="TableColor.cs" lineNumbers="true" %}
```csharp
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, bool SeparateRows = true, List<CellOptions> CellOptions = null)
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, KernelColorType colorTypeSeparatorForeground, KernelColorType colorTypeHeaderForeground, KernelColorType colorTypeValueForeground, KernelColorType colorTypeBackground, bool SeparateRows = true, List<CellOptions> CellOptions = null)
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, ConsoleColors SeparatorForegroundColor, ConsoleColors HeaderForegroundColor, ConsoleColors ValueForegroundColor, ConsoleColors BackgroundColor, bool SeparateRows = true, List<CellOptions> CellOptions = null)
public static void WriteTable(string[] Headers, string[,] Rows, int Margin, Color SeparatorForegroundColor, Color HeaderForegroundColor, Color ValueForegroundColor, Color BackgroundColor, bool SeparateRows = true, List<CellOptions> CellOptions = null)
```
{% endcode %}

**Tried to balance color support for writers**

Migration from `ConsoleColor` to `ConsoleColors` is complete. This means that all the writers in the `KS.Misc.*Writers` now have the `ConsoleColors` support.

The latest ColorSeq version, 1.0.2, will be used to make it easier to achieve.

{% hint style="info" %}
It's best to upgrade your ConsoleColor variables to ConsoleColors at minimum.
{% endhint %}

**Renamed command executor and base to reduce confusion**

{% code lineNumbers="true" %}
```visual-basic
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

**Renamed ConsoleSanityChecker to ConsoleChecker**

{% code title="ConsoleSanityChecker.vb" lineNumbers="true" %}
```visual-basic
Public Module ConsoleSanityChecker
```
{% endcode %}

This class will be filled by many console checks, so renamed it according to the purpose.

{% hint style="info" %}
To use the methods inside the class, rename the references from `ConsoleSanityChecker` -> `ConsoleChecker`.
{% endhint %}

**WriteWherePlain from TextWriterWhereColor renamed**

{% code title="TextWriterWhereColor.vb" lineNumbers="true" %}
```visual-basic
Public Sub WriteWherePlain(msg As String, Left As Integer, Top As Integer, ParamArray vars() As Object)
Public Sub WriteWherePlain(msg As String, Left As Integer, Top As Integer, [Return] As Boolean, ParamArray vars() As Object)
```
{% endcode %}

This change is necessary to fit in with the rest of the ConsoleWriters

{% hint style="info" %}
To continue using the plain writer, rename the references from `WriteWherePlain` -> `WriteWhere`.
{% endhint %}

**Removed Screensaver.colors**

{% code title="Screensaver.vb" lineNumbers="true" %}
```visual-basic
Public ReadOnly colors() As ConsoleColor = CType([Enum].GetValues(GetType(ConsoleColor)), ConsoleColor())
Public ReadOnly colors255() As ConsoleColors = CType([Enum].GetValues(GetType(ConsoleColors)), ConsoleColors())
```
{% endcode %}

This is to remove support for 255 colors in screensavers.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

**Moved KS.Network classes to KS.Network.Base**

{% code lineNumbers="true" %}
```visual-basic
Public Module NetworkAdapter
Public Module NetworkAdapterPrint
Public Module NetworkTools
```
{% endcode %}

These classes are believed to be the base classes for the networking. These classes are used for general networking purposes.

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Network` to `KS.Network.Base`.
{% endhint %}

**Condensed speed dial to KS.Network.SpeedDial**

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

**Moved network transfer functions to KS.Network.Base.Transfer**

{% code lineNumbers="true" %}
```visual-basic
Public Module NetworkTransfer
Public Class NetworkTransferInfo
Public Enum NetworkTransferType
```
{% endcode %}

We've done that to the base network classes, so why not do the same to the network transfer functions?

{% hint style="info" %}
Change the namespace declaration to refer to this enumeration from `KS.Network.Transfer` to `KS.Network.Base.Transfer`.
{% endhint %}

**Kernel exception handling changed**

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

**Changed GetFilteredPositions to tuple**

{% code title="ConsoleExtensions.vb" lineNumbers="true" %}
```visual-basic
Public Sub GetFilteredPositions(Text As String, ByRef Left As Integer, ByRef Top As Integer, ParamArray Vars() As Object)
```
{% endcode %}

To aid in simplicity of the function, we've replaced the two reference variables with the tuples in their respective orders of cursor left and top positions.

{% hint style="info" %}
The first tuple value in the returned value specifies the filtered X position, and the second one specifies the filtered Y position in the console buffer.
{% endhint %}

{% code title="ConsoleExtensions.cs" lineNumbers="true" %}
```csharp
public static (int, int) GetFilteredPositions(string Text, params object[] Vars)
```
{% endcode %}

**Internalized several kernel tools**

{% code title="KernelTools.vb" lineNumbers="true" %}
```visual-basic
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

**Removed PrepareDict**

{% code title="Translate.vb" lineNumbers="true" %}
```visual-basic
Public Function PrepareDict(lang As String) As Dictionary(Of String, String)
```
{% endcode %}

PrepareDict used to populate the string dictionary with definitions to the localized string. Now, because the language management routine was remodeled, we've removed PrepareDict as part of the change.

{% hint style="danger" %}
The language manager automatically does this each time your mod sets the language, so we advice you to cease using this function.
{% endhint %}

**Removed network adapter querying**

{% code lineNumbers="true" %}
```visual-basic
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

**Theme preview is no longer exclusive to theme studio**

{% code title="ThemeStudioTools.vb" lineNumbers="true" %}
```visual-basic
Sub PreparePreview()
```
{% endcode %}

The theme preview routine used to depend on the theme studio to do its job, under the name of `ThemeStudioTools.PreparePreview()`. However, because there were recent improvements to the theming system, we've finally condensed the preview routine to `ThemeTools.PreviewTheme()`. You can no longer use the old method, because it also required loading the theme information to the theme studio itself. What if it was called in a context that has no relationship with the theme studio, such as in the case of `themesel`?

{% hint style="info" %}
You can use the new `ThemeTools.PreviewTheme()` function to preview any theme. The method signatures are written below.
{% endhint %}

{% code title="ThemeTools.cs" lineNumbers="true" %}
```csharp
public static void PreviewTheme(string theme)
public static void PreviewTheme(ThemeInfo theme)
public static void PreviewTheme(Dictionary<KernelColorType, Color> colors)
```
{% endcode %}

**Migrated kernel arguments**

{% code lineNumbers="true" %}
```visual-basic
Public Enum ArgumentType
Public Module CommandLineArgs
Public Module ArgumentPrompt
```
{% endcode %}

We used to provide two argument channels: one for the command-line kernel arguments, and one for the kernel arguments. The entry point has been provided the `Args` variable to get all the arguments from the command line. Since it has undergone recent improvements to the system, we've decided to remove the kernel arguments channel, so we don't have to parse the passed arguments twice.

We also had to remove the `arginj` command, one of the commands that made appearance in first-generation versions of KS.

**Removed GetCompilerVars**

{% code title="KernelTools.vb" lineNumbers="true" %}
```visual-basic
Public Function GetCompilerVars() As String()
```
{% endcode %}

This was only useful in conditions where getting the compiler variables for determining the kernel milestone is needed, which was seldom needed by mods. We've removed it.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

**Migrated encryptors to Kernel Drivers**

The kernel drivers are beneficial, so we decided to give the encryptors a chance to appear in kernel drivers. This caused us to remove `EncryptionAlgorithms` and `IEncryptor` and replace them with `IEncryptionDriver`, handled by the kernel driver handler.

{% hint style="info" %}
You can implement your own encryptor by registering your custom encryption driver using the RegisterDriver function.
{% endhint %}

{% code title="DriverHandler.cs" lineNumbers="true" %}
```csharp
public static void RegisterDriver(DriverTypes type, IDriver driver)
```
{% endcode %}

**Removed TwoNewlines argument from WriteLicense**

{% code title="WelcomeMessage.vb" lineNumbers="true" %}
```visual-basic
Sub WriteLicense(TwoNewlines As Boolean)
```
{% endcode %}

This argument was unused, so we decided to remove it from `WriteLicense()`.

{% hint style="danger" %}
We advice you to cease using this variable.
{% endhint %}

**Renamed PartInfo to ModPartInfo**

{% code title="PartInfo.vb" lineNumbers="true" %}
```visual-basic
Public Class PartInfo
```
{% endcode %}

Add `Mod` next to `PartInfo` to clarify which module uses this.

{% hint style="info" %}
To implement your new mod parts, construct the ModPartInfo class. For existing mod parts, rename PartInfo to ModPartInfo.
{% endhint %}

**Manual pages moved to Modifications**

{% code lineNumbers="true" %}
```visual-basic
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

**Changed Notifications to NotificationManager**

{% code title="Notifications.vb" lineNumbers="true" %}
```visual-basic
Public Module Notifications
```
{% endcode %}

We felt that both the `Notification` and `Notifications` classes are confusing for some people, so we decided to make these clearer by renaming the `Notifications` class to `NotificationManager`

{% hint style="info" %}
To use the methods inside the class, rename the references from `Notifications` -> `NotificationManager`.
{% endhint %}

**Removed getting property value in variable**

{% code title="PropertyManager.vb" lineNumbers="true" %}
```visual-basic
Public Function GetPropertyValueInVariable(Variable As String, [Property] As String) As Object
Public Function GetPropertyValueInVariable(Variable As String, [Property] As String, VariableType As Type) As Object
```
{% endcode %}

VariableProperty is no longer used, so we decided to remove it. As a consequence, we also had to remove the `PropertyManager.GetPropertyValueInVariable()` routine.

{% hint style="danger" %}
We advice you to cease using these functions.
{% endhint %}

**Moved ColTypes to KernelColorType**

{% code title="ColorTools.vb" lineNumbers="true" %}
```visual-basic
Public Enum ColTypes As Integer
```
{% endcode %}

This is an enumeration which simply tells the difference of all the defined and known kernel color types. We have moved ColTypes to KernelColorType.

{% hint style="info" %}
To continue using the kernel color type enumeration, rename the references from `ColTypes` to `KernelColorType`, importing the `KS.ConsoleBase.Colors` namespace.
{% endhint %}

{% code title="KernelColorType.cs" lineNumbers="true" %}
```csharp
public enum KernelColorType
```
{% endcode %}

**Removed ref from conditional debug writers**

{% code title="DebugWriter.vb" lineNumbers="true" %}
```visual-basic
Public Sub WdbgConditional(ByRef Condition As Boolean, Level As DebugLevel, text As String, ParamArray vars() As Object)
Public Sub WStkTrcConditional(ByRef Condition As Boolean, Ex As Exception)
```
{% endcode %}

The conditional debug writers didn't do anything to the boolean condition that caused it to change its state, so we decided to pass the boolean value by value and not by reference.

{% hint style="info" %}
Remove the `ref` prefix from the boolean variable that is being tested from your conditional debug writer calls. Follow the below method signatures:
{% endhint %}

{% code title="DebugWriters.cs" lineNumbers="true" %}
```csharp
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object[] vars)
public static void WriteDebugStackTraceConditional(bool Condition, Exception Ex)
```
{% endcode %}

**Removed GroupManagement (a.k.a. PermissionManagement)**

{% code title="PermissionManagement.vb" lineNumbers="true" %}
```visual-basic
Public Module PermissionManagement
```
{% endcode %}

The GroupManagement module was removed in preparation for the new permission system. The groups were moved outside in the users JSON file to become singular boolean variables, and the permission system was implemented under the `KS.Users.Permissions` namespace.

{% hint style="info" %}
To grant or revoke individual permissions from a specified user, use the following functions:

* `GrantPermission`
* `RevokePermission`

You may need to import the `KS.Users.Permissions` namespace to use this feature, although it works on small permissions, unlike the superuser variable which grants all permissions.

Their method signatures are written below.
{% endhint %}

{% code title="PermissionsTools.cs" lineNumbers="true" %}
```csharp
public static void GrantPermission(string User, PermissionTypes permissionType)
public static void RevokePermission(string User, PermissionTypes permissionType)
```
{% endcode %}

**Removed obsolete functions**

{% code lineNumbers="true" %}
```visual-basic
'Input.vb
Public Function ReadLineUntil(ByRef Condition As Boolean) As String

'ThreadManager.vb
Public Sub SleepNoBlock(Time As Long, ThreadWork As BackgroundWorker)

'NetworkTools.vb
Public Sub ConvertSpeedDialEntries(SpeedDialType As SpeedDialType)
```
{% endcode %}

`ReadLineUntil()`, `SleepNoBlock()`, and `ConvertSpeedDialEntries()` were removed for being obsolete. The first function was removed in favor of ReadLine.Reboot and TermRead, the second function was removed for the absence of our usage of `BackgroundWorker`, and the third function was removed as a result of huge improvements to the speed dial functionality that makes it incompatible with the older speed dial format.

{% hint style="danger" %}
We advice you to cease using these functions.
{% endhint %}

{% hint style="warning" %}
To sleep without blocking, convert all your BackgroundWorkers to KernelThread and use the appropriate SleepNoBlock overload for your kernel thread. The below method signature is shown.
{% endhint %}

{% code title="ThreadManager.cs" lineNumbers="true" %}
```csharp
public static void SleepNoBlock(long Time, KernelThread ThreadWork)
```
{% endcode %}

{% hint style="warning" %}
You may have to convert your speed dial entries manually. The instructions will be done soon. Please stay tuned!
{% endhint %}

#### Argument auto-completion re-implemented

{% code title="CommandArgumentInfo.vb" lineNumbers="true" %}
```visual-basic
Public Sub New(HelpUsages() As String, ArgumentsRequired As Boolean, MinimumArguments As Integer, Optional AutoCompleter As Func(Of String()) = Nothing)
```
{% endcode %}

Command auto-completion used to be available on ReadLine.Reboot to automatically complete the command needed to run. However, ReadLine.Reboot has come to an end, so we decided to re-implement it to align with TermRead.

As a result, the auto completion facility in your shell, if it has one implemented in your `CommandArgumentInfo`, will have to be re-implemented to parse the whole command passed to the auto-completion builder, `AutoCompleter`, and generate suggestions based on that data.

In your `CommandInfo` implementation of your command, you'll also have to re-implement it so that the auto-completer takes three arguments. You can always discard the index and delimiters argument in your action declaration: `(Text, _, _) => Function(Text)`.

{% code title="CommandArgumentInfo.cs" lineNumbers="true" %}
```csharp
public CommandArgumentInfo(string[] HelpUsages, bool ArgumentsRequired, int MinimumArguments, Func<string, int, char[], string[]> AutoCompleter = null)
```
{% endcode %}

### Converted kernel exceptions

Previously, we've used the built-in .NET exceptions to catch appropriate exceptions based on the context of an error. Since `KernelException` was implemented as part of the first development semester of Nitrocid KS 0.1.0, we decided to throw all the exceptions to `KernelException` that dynamically provides extended information as to what's wrong, coupled together with possible suggestions and extra messages.

{% hint style="info" %}
In order to throw these exceptions, you must now route all your exception handlers in your mods to target `KernelException` and check the exception type before you can take action. Converted exceptions are found in [this commit](https://github.com/Aptivi/Kernel-Simulator/commit/1d4d31cd12087659b807687d286047013a22273b).
{% endhint %}

### Removed decisive writers

{% code title="Decisive.vb" lineNumbers="true" %}
```visual-basic
Public Sub DecisiveWrite(CommandType As ShellType, DebugDeviceSocket As StreamWriter, Text As String, Line As Boolean, colorType As ColTypes, ParamArray vars() As Object)
```
{% endcode %}

We used to implement the decisive writers to decide whether to use the normal console writer or to use the remote debug connection according to the shell type. Over time, the remote debug shell was removed and later implemented as a standalone add-on for the remote debugger. This leads to us removing this decisive writer from the `MiscWriters` namespace.

{% hint style="danger" %}
We advice you to cease using this function.
{% endhint %}

### Moved `PlaceParse` to `KS.Misc.Probers.Placeholder`

{% code title="PlaceParse.vb" lineNumbers="true" %}
```visual-basic
Public Module PlaceParse
```
{% endcode %}

This module used to statically replace all the text placeholders found within the text with their values. It used to exist in the `KS.Misc.Probers` namespace, but we moved it to the `KS.Misc.Probers.Placeholder` namespace to align with the latest Nitrocid KS API design. It also earned a new way to dynamically parse the placeholders.

{% hint style="info" %}
The function names and the module itself are unchanged, but we just need you to change the namespace import to the abovementioned namespace.
{% endhint %}

### Removed `KernelColorType.Gray`

{% code title="ColorTools.vb" lineNumbers="true" %}
```visual-basic
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

### Replaced `GetVariables()` with `Variables` property

{% code title="UESHVariables.vb" lineNumbers="true" %}
```visual-basic
Public Function GetVariables() As Dictionary(Of String, String)
```
{% endcode %}

This function used to return a list of available UESH variables. It's been replaced with a property that does exactly the same thing. It's to make your mod code related to UESH variables easier to read.

{% hint style="info" %}
Replace all calls to `UESHVariables.GetVariables()` with `Variables`.
{% endhint %}

### Removed remote-debug-related argument from `ShowHelp()`

{% code title="HelpSystem.vb" lineNumbers="true" %}
```visual-basic
Public Sub ShowHelp(command As String, CommandType As ShellType, Optional DebugDeviceSocket As StreamWriter = Nothing)
                                                                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
{% endcode %}

Remote debug shell used to require the `DebugDeviceSocket` parameter to be passed to `ShowHelp` for `DecisiveWriter` to decide what type of console is going to be written to. Since `DecisiveWriter` got removed and the remote debug shell was re-implemented to be standalone, we decided to remove this parameter.

{% hint style="info" %}
There was no need to pass `DebugDeviceSocket` to this function anyways. If you really need to use it, make your own remote debug command with the help entry, and Nitrocid KS will take care of the rest.
{% endhint %}

### Renamed few classes

{% code title="TimeDate.vb" lineNumbers="true" %}
```visual-basic
Namespace TimeDate
    Public Module TimeDate
```
{% endcode %}

{% code title="IScript.vb" lineNumbers="true" %}
```visual-basic
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

### From 0.1.0 Beta 1

#### Employed `ColorPrint.Core` for color wheel

{% code title="ColorWheelOpen.vb" lineNumbers="true" %}
```visual-basic
Namespace ConsoleBase.Colors
    Public Module ColorWheelOpen
```
{% endcode %}

The color wheel was implemented in the kernel to allow color selection. However, it lacked features such as the color blindness simulation, so we decided to make an entirely new library dedicated to this. As a result, we've replaced the kernel's implementation with `ColorPrint.Core`, which is more portable and easier to use.

{% hint style="info" %}
Merge your calls to the `ColorWheelOpen` class to `ColorPrint.Core` as it's easier to use and more portable than the former class.
{% endhint %}

#### Removed the country-based RSS feed selector

{% code title="RSSTools.cs" lineNumbers="true" %}
```csharp
public static void OpenFeedSelector()
```
{% endcode %}

The feed selector used to prompt you for a country so that you can select a feed according to the minimal list of known RSS feeds operating from the selected country. Recently, we've discovered many broken links (404's) across many feeds, so we decided to remove it as the source was out of date.

{% hint style="warning" %}
Its functionality will be replaced with the bookmarked feed selector. Meanwhile, it's advisable to stop using this function on your mods.
{% endhint %}

#### Removed `UseCtrlCAsInput` from `ReadLine()`'s

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static string ReadLine(bool UseCtrlCAsInput)
public static string ReadLine(string InputText, string DefaultValue, bool UseCtrlCAsInput)
public static string ReadLineUnsafe(string InputText, string DefaultValue, bool UseCtrlCAsInput)
```
{% endcode %}

`UseCtrlCAsInput` used to tell ReadLine.Reboot to treat `Ctrl + C` as input to try to aid in cancelling prompts. Apparently, that library was deprecated and replaced with TermRead. As a result, this feature is removed.

{% hint style="danger" %}
We advice you to cease using this variable in the above functions.
{% endhint %}

#### Removed `SaveCurrDir()`

{% code title="CurrentDirectory.cs" lineNumbers="true" %}
```csharp
public static void SaveCurrDir()
public static bool TrySaveCurrDir()
```
{% endcode %}

This function used to save the current directory value to the kernel configuration file stored in the `%LOCALAPPDATA%/KS/KernelMainConfig.json` for Windows or the `$HOME/.config/ks/KernelMainConfig.json`. Following the recent improvements in the configuration system that took place two times during 0.1.0's development, the `SaveCurrDir()` function was effectively reduced to a single call to the `Config.CreateConfig()` function, which already deals with this kind of change, rendering this function useless. As a result, we decided to remove this function as it added no value and was just an extraneous wrapper function.

{% hint style="warning" %}
If you want to save the current directory value in the future, please use the kernel settings application to save the configuration. Programmatically, you'll have to call the `Config.CreateConfig()` function instead of the two above functions.
{% endhint %}

#### Group system and the User Management API

{% code title="UserManagement.cs" lineNumbers="true" %}
```csharp
public static void LoadUserToken()
public static JToken GetUserProperty(string User, UserProperty PropertyType)
public static void SetUserProperty(string User, UserProperty PropertyType, JToken Value)
public static void InitializeSystemAccount()
```
{% endcode %}

We've added a real group system to the KS.Users namespace under Groups in order to group the users and give them shared permissions. In consequence, we had to rework the user management system, causing several API removals.

The following functions were documented:

* `LoadUserToken()`: Tries to manually deserialize the user configuration JSON file to be usable with all the user management functions.
* `InitializeSystemAccount()`: Tries to initialize a root account with a defined password from the same user token.
* `GetUserProperty()`: Gets a user property as a JSON token, JToken, which has to be manually cast to either a string, boolean, or array of strings.
* `SetUserProperty()`: Sets a user property, taking an uncasted JSON token that represents either a string, boolean, or array of strings.

The first two functions were removed, because they were deemed to be unnecessary for a long time. A re-work to the user management API made it reasonable to remove these functions.

However, the last two functions were removed because it was found to be complicated for having to cast to their appropriate types manually. We also removed the ability to directly set a user's properties security-wise.

{% hint style="danger" %}
Because the user management API reached to a stage when it was re-written to simplify things, we advice you to cease using these functions.
{% endhint %}

#### Initial implementation of the TUI

The following classes are affected:

{% code lineNumbers="true" %}
```csharp
public static class ContactsManagerCli
public static class TaskManagerCli
public static class FileManagerCli
```
{% endcode %}

The following functions are affected:

{% code lineNumbers="true" %}
```csharp
public static void OpenMain()
```
{% endcode %}

The three CLIs used to implement their own CLI based on data for contacts, kernel threads, and files respectively. Now, with the introduction of the `IInteractiveTui` interface and the `BaseInteractiveTui` class, we've made the three above classes implement both the classes, removing the `static` modifier from the three CLIs.

As a result, we've removed the `OpenMain()` function from all of them. However, you can still open the CLI as follows:

{% code lineNumbers="true" %}
```csharp
InteractiveTuiTools.OpenInteractiveTui(new ContactsManagerCli());
InteractiveTuiTools.OpenInteractiveTui(new TaskManagerCli());
InteractiveTuiTools.OpenInteractiveTui(new FileManagerCli());
```
{% endcode %}

This removal was necessary to avoid code repetition, effectively making maintenance easier.

{% hint style="info" %}
If you want to open the three CLIs, refer to the above code snippet about the usage of `OpenInteractiveTui()`.
{% endhint %}

#### Added warning reports to the splash interface

{% code title="ISplash.cs" lineNumbers="true" %}
```csharp
void ReportWarning(int Progress, string WarningReport, Exception ExceptionInfo, params object[] Vars);
```
{% endcode %}

The splash reporter used to only report the progress and the error messages during the kernel startup. Now, we've added warnings to extend the possibility of accurately reporting warnings without having to rely on special conditions on the progress report.

{% hint style="info" %}
Mods that implement splashes now have to implement the above function to be able to report warnings.
{% endhint %}

#### Added `ReadToEndAndSeek()` to filesystem driver

{% code title="IFilesystemDriver.cs" lineNumbers="true" %}
```csharp
string ReadToEndAndSeek(ref StreamReader stream);
```
{% endcode %}

As part of the removal of Extensification dependency from Nitrocid KS as a result of its deprecation, we decided to adapt the kernel to remove all references to Extensification and re-implement things. The commit states:

> Since this library is deprecated starting today, we've removed all references to Extensification by updating all libraries and making necessary changes to the API to restore the used Extensification functions to `TextTools`, `IntegerTools`, and `StreamRead`. Custom filesystem drivers in your mods will now have to implement `ReadToEndAndSeek()` to be compatible with this revision of N-KS, so we've increased the mod API version to `3.0.25.7`.

{% hint style="info" %}
Mods that implement filesystem drivers now have to implement the above function to be able to be installed on N-KS mod API 3.0.25.7 or later.
{% endhint %}

#### Removed `ConsoleWrapper.WindowTop`

{% code title="ConsoleWrapper.cs" lineNumbers="true" %}
```csharp
public static int WindowTop
```
{% endcode %}

`Console.WindowTop` is always 0 on both the Windows and the Unix operating systems, but you can set this value only on Windows systems, which kills the potential of cross-platform. This is deemed unnecessary for most of the things, which makes it redundant, so we've removed this function from both the `ConsoleWrapper` and the `Console` driver.

{% hint style="danger" %}
We advice you to replace all instances of this function from `ConsoleWrapper` with `0`, and remove all implementations of this property from all your `Console` drivers.
{% endhint %}

#### Converted string char variables to chars

{% code lineNumbers="true" %}
```csharp
public string CustomUpperLeftCornerChar { get; set; } = "╔";
public string CustomUpperRightCornerChar { get; set; } = "╗";
public string CustomLowerLeftCornerChar { get; set; } = "╚";
(...)
```
{% endcode %}

The above char variables used to hold only one character, but they were defined as strings instead of chars, so users made it possible to place more than one character to these variables. Usually, the handlers only take the first character from the string.

Since the config entries defined these variables as configurable under the `SChar` type, the config app made enough checking to make sure that only one character can be input. This caused us to convert all these variables to strings, affecting the following classes:

* `NotificationManager`
* `Notification`
* `BarRotSettings`
* `IndeterminateSettings`
* `ProgressClockSettings`
* `RampSettings`
* `BorderTools`
* `ProgressTools`

The following writers are also affected and are found to be using characters as strings before the change:

* `WriteBorder`() and `WriteBorderPlain`()
* `WriteBoxFrame`() and `WriteBoxFramePlain`()
* `WriteInfoBox`() and `WriteInfoBoxPlain`()
* `WriteProgress`() and `WriteProgressPlain`()
* `WriteVerticalProgress`() and `WriteVerticalProgressPlain`()

{% hint style="info" %}
For mods that treat characters as strings and use one of the above classes and variables that hold only one character, you'll have to refactor the logic to treat these characters as chars. However, if you use char variables and convert them to string in either the writers or the char variables, such as `CustomLowerLeftCornerChar`, you'll no longer need to convert your char variables to strings.
{% endhint %}

#### Added finding files using regular expressions

The following functions are added to the filesystem driver:

{% code title="IFilesystemDriver.cs" lineNumbers="true" %}
```csharp
string[] GetFilesystemEntriesRegex(string Parent, string Pattern, bool Recursive = false);
```
{% endcode %}

This function gets all the filesystem entries found under the specified parent directory, with the regular expression pattern. This uses the regular expression driver to handle the regex work.

{% hint style="info" %}
Mods that implement filesystem drivers now have to implement the above function to be able to use it. It's also advisable to use the regex driver in the function implementation.
{% endhint %}

#### Removed configurable maintenance mode

{% code title="Flags.cs" lineNumbers="true" %}
```csharp
public static bool Maintenance
```
{% endcode %}

Long ago, we used to allow users to force the kernel to maintenance mode upon setting this value right from the configuration application. However, this can be abused, so we decided to remove it as a configuration entry, but the mode itself stays. You can still run the kernel in maintenance mode by passing `maintenance` as a command line argument to Nitrocid's entry point. Refer to the below page for more information:

{% content-ref url="../../advanced-and-power-users/inner-workings/kernel-arguments.md" %}
[kernel-arguments.md](../../advanced-and-power-users/inner-workings/kernel-arguments.md)
{% endcontent-ref %}

{% hint style="danger" %}
We advice you to cease using this flag. Maintenance mode doesn't allow mods to load, anyways.
{% endhint %}

#### Migrated two speed dial types to one JSON file

{% code title="Paths.cs" lineNumbers="true" %}
```csharp
public static string FTPSpeedDialPath
public static string SFTPSpeedDialPath
```
{% endcode %}

{% code title="PathType.cs" lineNumbers="true" %}
```csharp
/// <summary>
/// FTP speed dial file.
/// </summary>
FTPSpeedDial,
/// <summary>
/// SFTP speed dial file.
/// </summary>
SFTPSpeedDial,
```
{% endcode %}

{% code title="SpeedDialTools.cs" lineNumbers="true" %}
```csharp
public static KernelPathType GetPathTypeFromSpeedDialType(SpeedDialType SpeedDialType)
public static JObject GetTokenFromSpeedDial(SpeedDialType SpeedDialType)
public static Dictionary<string, JToken> ListSpeedDialEntries(SpeedDialType SpeedDialType)
public static JToken GetQuickConnectInfo(SpeedDialType SpeedDialType)
```
{% endcode %}

To migrate two different JSON files holding speed dial entries for FTP and SFTP servers, we decided to replace `FTPSpeedDial` and `SFTPSpeedDial` with `SpeedDial` and `FTPSpeedDialPath` and `SFTPSpeedDialPath` with `SpeedDialPath`, effectively removing a function from `SpeedDialTools`, `GetPathTypeFromSpeedDialType()`, and the remaining functions removing the `(SpeedDialType SpeedDialType)` signature, causing them not to take any speed dial type.

The commit said:

> This migration is necessary to efficiently put speed dials to one JSON file as we have the Type key already in speed dial properties.

{% hint style="info" %}
We advice you to replace all calls to type-specific enumerations and paths with a single speed dial enumeration value, `SpeedDial`, and path, `SpeedDialPath`, respectively. Also, we advice you to use the three functions that stay, but without the type, and cease using the `GetPathTypeFromSpeedDialType()` function.
{% endhint %}

#### Added support for SwitchInfo

{% code title="CommandArgumentInfo.cs" lineNumbers="true" %}
```csharp
public HelpUsage[] HelpUsages { get; private set; }
public CommandArgumentInfo(string[] HelpUsages, bool ArgumentsRequired, int MinimumArguments, Func<string, int, char[], string[]> AutoCompleter = null)
public CommandArgumentInfo(HelpUsage[] HelpUsages, bool ArgumentsRequired, int MinimumArguments, Func<string, int, char[], string[]> AutoCompleter = null)
```
{% endcode %}

{% code title="HelpUsage.cs" lineNumbers="true" %}
```csharp
public class HelpUsage
```
{% endcode %}

`CommandArgumentInfo` and the UESH shell used to hold `HelpUsage` classes to get info about help usages, but they didn't become aware of unknown switches, so we decided to split `HelpUsage` to a string of command arguments and command switches, using `SwitchInfo` as a class to hold help information for each switch, including the properties for each switch, like the requirement and the value requirement.

This causes us to remove all help helpers that hold info about the supported switches, especially since the later commands that do support switches didn't have their help helpers that tell the users about the command switches.

In consequence, `CommandArgumentInfo` has been changed to hold only one constructor that holds both array of arguments and array of switch information class instances.

{% hint style="info" %}
We advice you to use the below constructor to accommodate the above changes made:

```csharp
public CommandArgumentInfo(string[] Arguments, SwitchInfo[] Switches, bool ArgumentsRequired, int MinimumArguments, Func<string, int, char[], string[]> AutoCompleter = null)
```
{% endhint %}

An example is provided below:

{% code title="Snippet from UESHShellInfo.cs" lineNumbers="true" %}
```csharp
{ "find", new CommandInfo("find", ShellType, "Finds a file in the specified directory or in the current directory",
    new CommandArgumentInfo(new[] { "file", "directory" }, new[] { new SwitchInfo("recursive", "Searches for a file recursively"), new SwitchInfo("exec", "Executes a command on a file", false, true) }, true, 1), new FindCommand()) },
```
{% endcode %}

#### Migrated text tools

{% code title="Deleted classes" lineNumbers="true" %}
```csharp
public static class StringManipulate
public static class StringQuery
```
{% endcode %}

As `TextTools` matured with different string tools, we decided to migrate the following functions from their respective classes to that class under the `KS.Misc.Text` namespace:

* `FormatString(string Format, params object[] Vars)`
* `IsStringNumeric(string Expression)`

{% hint style="info" %}
As a result, we advice you to use the `TextTools` class to execute the above two functions. Their signatures and behavior remains unchanged. This means removing any reference to the two classes found under the `KS.Misc.Reflection` namespace.
{% endhint %}

#### Moved `BannerFigletFont` to `WelcomeMessage`

{% code title="KernelTools.cs" lineNumbers="true" %}
```csharp
public static string BannerFigletFont =>
    Config.MainConfig.BannerFigletFont;
```
{% endcode %}

As this property doesn't have to do with the kernel tools, we decided to move from the `KernelTools` class to the `WelcomeMessage` class found under the `KS.Misc.Writers.MiscWriters` namespace.

{% hint style="info" %}
If you want to continue using this property, we suggest that you change the `using KS.Kernel` line to replace the namespace with the `KS.Misc.Writers.MiscWriters` namespace in order to be able to reference `BannerFigletFont` under `WelcomeMessage`.
{% endhint %}

#### Easier way to render info into the second pane

{% code title="IInteractiveTui.cs" lineNumbers="true" %}
```csharp
public string RenderInfoOnSecondPane(object item)
```
{% endcode %}

When we first introduced the interactive TUI feature, we had to leave the entire "rendering to the second pane" logic to your interactive TUI instance. However, since this involves having to wrap the informational pane and to work out the text lengths and console positions yourself, we've placed these requirements so that it's up to the handler to handle printing the information, effectively replacing the function above with `GetInfoFromItem`.

{% hint style="info" %}
It's now easier to render the information pane using just your text! Just form your final informational text by implementing the `GetInfoFromItem` function to return said information. The function signature is found below:

```csharp
public string GetInfoFromItem(object item)
```
{% endhint %}

#### Enhanced the screen locking feature

{% code title="Login.cs" lineNumbers="true" %}
```csharp
public static void ShowPasswordPrompt(string usernamerequested)
```
{% endcode %}

The screen locking feature was malfunctioning for a long time. Unfortunately, it went under the radar, so it wasn't looked at. We've finally managed to enhance the screen locking feature by checking our heuristics. Moreover, we had to separate the `ShowPasswordPrompt` function from trying to log the user in, as this was the requirement in enhancing the screen lock, since it was used by this feature.

{% hint style="info" %}
The `ShowPasswordPrompt` function now contains a return type of `bool`, which returns `true` if the password was valid or if the user database concluded that the password was empty, and `false` if the password was invalid. The new signature is now:

{% code title="Login.cs" lineNumbers="true" %}
```csharp
public static bool ShowPasswordPrompt(string usernamerequested)
```
{% endcode %}
{% endhint %}

#### Moved journaling related classes to `KS.Kernel.Journaling`

{% code title="JournalManager.cs, JournalStatus.cs" lineNumbers="true" %}
```csharp
namespace KS.Kernel.Administration.Journalling
```
{% endcode %}

We used to place all the journaling-related classes and tools to the `KS.Kernel.Administration.Journalling` namespace, until we've found out that said namespace wasn't needed because we didn't have plans to add another namespace to the `Administration` namespace, so we decided to move journaling-related classes to the `KS.Kernel.Journaling` namespace.

{% hint style="info" %}
To continue using these journaling classes, you have to change the `using` statements to point to `KS.Kernel.Journaling`.
{% endhint %}

#### Time and Date API enhancements

{% code title="Old TimeDate namespace" lineNumbers="true" %}
```csharp
namespace KS.TimeDate
```
{% endcode %}

The TimeDate API was left untouched for a long time, and its structure was a bit too old for the modern API system that Nitrocid KS uses to be usable for mods and general purpose, so we have decided to create the following namespaces:

* `KS.Kernel.Time.Converters`
* `KS.Kernel.Time.Renderers`
* `KS.Kernel.Time.Timezones`
* `KS.Kernel.Time`

We have moved relevant functions according to their action to the above namespaces. For example, the `Render()` function was moved to `TimeDateRenderers` class in the `Renderers` namespace.

We have also isolated the `FormatType` enumeration from the `TimeDateTools` class so that the mods don't have to reference the class name in order to access this enumeration.

Also, some functions like `GetRemainingTimeFromNow()` have their return types changed from `string` to `TimeSpan`. To get a string, you must now use the `RenderRemainingTimeFromNow()` function to continue using strings to render the remaining time from the current date and time.

{% hint style="info" %}
To keep using these functions, you must now change the imports in relevant code files to `KS.Kernel.Time` and its ancestors to be able to use their classes. You may need to adjust your usage of the functions and/or classes so that the behavior you're expecting remains unchanged.
{% endhint %}
