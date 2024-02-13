---
description: Guide for upgrading 0.1.0 RC mods to 0.1.0 Final
---

# ⬆ From 0.1.0 RC to 0.1.0 Final

This page lists all the changes that have been made from 0.1.0 RC to 0.1.0 Final. For upgrading your mods from 0.0.24.x directly to the 0.1.0 series, use the main upgrade page instead.

### Enumerable tools moved to EnumMagic

{% code title="EnumerableTools.cs" lineNumbers="true" %}
```csharp
public static class EnumerableTools
```
{% endcode %}

We've moved `EnumerableTools`, which holds non-generic enumerable interface tools that make jobs easier, from Nitrocid to EnumMagic as we needed to make it more open to the public. This is to ensure that these extensions get used by different libraries, such as Terminaux.

{% hint style="info" %}
You'll need to reference EnumMagic in order to use the tools.
{% endhint %}

### Moved three hashing algorithms

<pre class="language-csharp" data-title="DriverHandler.cs" data-line-numbers><code class="lang-csharp">internal static Dictionary&#x3C;DriverTypes, Dictionary&#x3C;string, IDriver>> drivers = new()
{
    (...)
    {
        DriverTypes.Encryption, new()
        {
            { "Default", new SHA256() },
<strong>            { "MD5", new MD5() },
</strong><strong>            { "SHA1", new SHA1() },
</strong>            { "SHA256", new SHA256() },
<strong>            { "SHA384", new SHA384() },
</strong>            { "SHA512", new SHA512() }
        }
    },
    (...)
}
</code></pre>

The three hashing algorithms have been moved to their own individual addons:

* `Nitrocid.Extras.Md5`
* `Nitrocid.Extras.Sha1`
* `Nitrocid.Extras.Sha384`

As a result, your mods will break if they assume that these three algorithms are installed as built-in, which is the case for RC and earlier beta versions of 0.1.0. The reason of that is because of security.

{% hint style="info" %}
Your mods will break only if they have been used and the three addons are not installed yet.
{% endhint %}

### Removed `SettingVariable` command flag

{% code title="CommandFlags.cs" lineNumbers="true" %}
```csharp
public enum CommandFlags
{
    (...)
    [Obsolete("-set=varname already exists. Use the AcceptsSet parameter from the CommandArgumentInfo constructor instead of this flag.")]
    SettingVariable = 8,
    (...)
}
```
{% endcode %}

We have introduced a new way to give your UESH commands an option to set a value to the UESH variable that is set by the `-set=varname` switch. This way, we've decided to remove `SettingVariable` in favor of the `AcceptsSet` parameter from the `CommandArgumentInfo` constructor.

{% hint style="danger" %}
From now on, you'll no longer be able to use the `SettingVariable` switch.
{% endhint %}

### Figlet tools class moved to Terminaux 3.0

{% code title="FigletTextTools.cs" lineNumbers="true" %}
```csharp
public static class FigletTextTools
```
{% endcode %}

The figlet text tools class has been moved to Terminaux 3.0, because we were working on a major version of Terminaux to aim for better experience for console applications, which promises many features to come, such as the transparent console support.

As for this change, it has been moved to this version of the terminal library to be able to manage default Figlet fonts in easier and more consistent ways.

{% hint style="info" %}
From now, use the `Config.MainConfig.DefaultFigletFontName` property while Terminaux 3.0 gets released.
{% endhint %}

### Removed obsolete functions from 0.1.0 RC

{% code title="KernelThread.cs" lineNumbers="true" %}
```csharp
public ulong NativeThreadId
```
{% endcode %}

{% code title="AliasManager.cs" lineNumbers="true" %}
```csharp
public static void ManageAlias(string mode, ShellType Type, string AliasCmd, string DestCmd = "")
public static void ManageAlias(string mode, string Type, string AliasCmd, string DestCmd = "")
```
{% endcode %}

{% code title="UESHCommands.cs" lineNumbers="true" %}
```csharp
public static class UESHCommands
```
{% endcode %}

The above functions have been obsoleted during the development cycle of 0.1.0. They have been removed in preparation for the final release of 0.1.0 for the below reasons:

* The native thread ID can't be get accurately, because managed threads and native threads don't have a 1:1 relationship with each other. Furthermore, one managed thread may use multiple operating system native threads. It's obtainable through the diagnostic library created by Microsoft, ClrMd, but we don't want to risk implementing it in fear of malicious mods using them to cause problems, such as re-implementing `Thread.Abort()` of some sort.
* The `ManageAlias()` functions were wrappers of the alias management functions. The wrapper functions appear to be doing nothing other than just being proxy functions with the mode as string declaring if we need to add or to remove an alias.
* The `UESHCommands` class was created to help mod developers set a UESH variable if they had `SettingVariable` enabled. However, `-set=varname` was implemented, resulting in both `UESHCommands` and `SettingVariable` being candidates for removal.

As a result, we've decided to remove them to clean things up.

{% hint style="info" %}
Here are some tips:

* As for the native thread ID, it won't be re-implemented.
* As for the `ManageAlias()` functions, they won't be re-implemented.
* As for the UESHCommands class, you can just use the `-set=varname` switch instead.
{% endhint %}

### Exact wording definition changed

{% code title="CommandArgumentPart.cs" lineNumbers="true" %}
```csharp
public string ExactWording { get; private set; }
public CommandArgumentPart(bool argumentRequired, string argumentExpression, Func<string[], string[]> autoCompleter = null, bool isNumeric = false, string exactWording = null)
```
{% endcode %}

{% code title="CommandArgumentPartOptions.cs" lineNumbers="true" %}
```csharp
public string ExactWording { get; set; }
```
{% endcode %}

Earlier, we've introduced exact wording option to the command argument to let the user know that this is the exact wording that they must write in order for the command to get executed. However, doing the same thing for more than one word was tedious, as you had to make many instances of `CommandArgumentInfo` to cover all the words.

As a result, we've decided to turn the definition of the two above variables to an array of strings that indicates what one of the words the user used to execute a command.

{% hint style="info" %}
You'll have to turn the declaration of this variable from a simple string to an array of strings, even if it's only one word.

```diff
 [
     new CommandArgumentPart(true, "tui", new CommandArgumentPartOptions()
     {
-        ExactWording = "tui"
+        ExactWording = ["tui"]
...
```
{% endhint %}

### Moved slow/wrapped writers to `TextDynamicWriters`

{% code title="TextWriters.cs" lineNumbers="true" %}
```csharp
public static void WriteSlowly(string msg, bool Line, double MsEachLetter, KernelColorType colorType, params object[] vars)
public static void WriteSlowly(string msg, bool Line, double MsEachLetter, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, KernelColorType colorType, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, bool Return, KernelColorType colorType, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, bool Return, int RightMargin, KernelColorType colorType, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, bool Return, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] vars)
public static void WriteWhereSlowly(string msg, bool Line, int Left, int Top, double MsEachLetter, bool Return, int RightMargin, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] vars)
public static void WriteWrapped(string Text, bool Line, KernelColorType colorType, params object[] vars)
public static void WriteWrapped(string Text, bool Line, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] vars)
```
{% endcode %}

We have moved all the above writers from `TextWriters` to its own separate class that contains all the dynamic writers, `TextDynamicWriters`. The dynamic writers can not be stored as a single string, so we've moved them as appropriate.

{% hint style="info" %}
None of the functions have been changed. You just need to update the reference to `TextWriters` to point to `TextDynamicWriters` instead.
{% endhint %}
