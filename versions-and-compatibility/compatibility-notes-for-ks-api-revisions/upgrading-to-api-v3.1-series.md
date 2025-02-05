---
icon: up
description: Follow the compatibility notes when upgrading your mods to API v3.1 series
---

# Upgrading to API v3.1 series

As API v3.1 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

## From 0.1.1 to 0.1.2 <a href="#from-0.0.24-to-0.1.0" id="from-0.0.24-to-0.1.0"></a>

This version gives your kernel a nice ink of paint that brings in feature additions and spectacular improvements in all fields, including some of the cosmetic changes.

### Updated Terminaux to 6.0 <a href="#updated-terminaux-to-6.0" id="updated-terminaux-to-6.0"></a>

We've updated Terminaux to 6.0 to bring improvements. However, this doesn't come without the cost of having to deal with the breaking changes, which, in this case, is many.

You can consult the list of breaking changes that result from upgrading to Terminaux 6.0 by pressing the below button:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v6.0" %}
[API v6.0](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v6.0)
{% endcontent-ref %}

### Detailed important changes <a href="#detailed-important-changes-2" id="detailed-important-changes-2"></a>

This section explains how to adapt the important changes to your mod code so that it works with 0.1.2 and higher. This highlights the most important changes that we have compiled for you.

#### **Removed modern debug log look**

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
public bool DebugLegacyLogStyle { get; set; } = true;
```
{% endcode %}

We have removed the modern debug log look introduced in the 0.1.0 series, because although it provided a more comfortable look for log reading, we've considered it as a flawed goal due to problems that may come with it, such as log timing differences.

{% hint style="danger" %}
It's advisable for you to stop using this feature.
{% endhint %}

#### **Removed `SplashDisplaysProgress`**

{% code title="BaseSplash.cs" lineNumbers="true" %}
```csharp
public virtual bool SplashDisplaysProgress => Info.DisplaysProgress;
```
{% endcode %}

{% code title="ISplash.cs" lineNumbers="true" %}
```csharp
bool SplashDisplaysProgress { get; }
```
{% endcode %}

The above property has been removed, because the `SplashInfo` instance already contains information about whether the splash displays progress information or not. This removal is necessary to maintain consistency.

{% hint style="danger" %}
It's advisable for you to stop using this property.
{% endhint %}

#### **Removed `ConfigCategory`**

{% code title="ConfigCategory.cs" lineNumbers="true" %}
```csharp
public enum ConfigCategory
```
{% endcode %}

This enumeration went unused as the 0.1.0 configuration has been remade with speed and serialization in mind. Therefore, it got removed as it's of no use. Also, it's limited to only specifying the categories in the main kernel configuration, none of which apply to other configurations, including the custom configuration instances that your mods may install.

{% hint style="info" %}
A viable alternative, `GetSettingsEntries()`, can be used to get the categories from all configurations.
{% endhint %}

#### **Merged `ListLanguages()` and `ListLanguagesWithCountry()` functions**

{% code title="LanguageManager.cs" lineNumbers="true" %}
```csharp
public static Dictionary<string, LanguageInfo> ListAllLanguagesWithCountry()
public static Dictionary<string, LanguageInfo> ListLanguagesWithCountry(string SearchTerm)
```
{% endcode %}

The above functions have been merged with the `ListLanguages()` function and it got an extra boolean parameter that does exactly the same thing. The reason was that because we wanted to avoid code repetition.

{% hint style="info" %}
If you still want to list languages with their countries in the key, you can now move to `ListLanguages`, passing `true` to the last optional argument.
{% endhint %}

#### **Aptivestigate is used for debugger and crash handler**

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
public bool DebugQuotaCheck { get; set; }
public int DebugQuotaLines { get; set; } = 10000;
```
{% endcode %}

As [Aptivestigate](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/ytZJv37OLeFyPEHQJtyw/) is now used to handle unhandled crashes and to facilitate the work of the debugger with the help of [Serilog](https://serilog.net/), which already provides the quota system, we've decided to remove the two above settings entries to improve log rotation.

As a consequence, you'll have to implement the `DebugLevel` argument in your debug logger implementation like this:

```csharp
public override void Write(string text, DebugLevel level)
{ }

public override void Write(string text, DebugLevel level, params object[] vars)
{ }
```

In addition to that, Aptivestigate uses the following paths to log the events:

* Windows: `%LOCALAPPDATA%/Aptivi/Logs`
* Unix: `~/.config/Aptivi/Logs`

This caused us to remove the `Debugging` kernel path to ensure that all logs that are logged by applications using Aptivestigate are logged in one place.

{% code title="KernelPathType.cs" lineNumbers="true" %}
```csharp
public enum KernelPathType
{
    (...)
    Debugging,
    (...)
}
```
{% endcode %}

{% code title="PathsManagement.cs" lineNumbers="true" %}
```csharp
public static string DebuggingPath
```
{% endcode %}

{% hint style="info" %}
Aptivestigate will continue to get updated, despite the low frequency of updates, which is expected. It will be expanded to allow you to control the logging behavior.
{% endhint %}

#### **Screensaver properties are get-only**

{% code title="IScreensaver.cs" lineNumbers="true" %}
```csharp
string ScreensaverName { get; set; }
bool ScreensaverContainsFlashingImages { get; set; }
```
{% endcode %}

{% code title="BaseScreensaver.cs" lineNumbers="true" %}
```csharp
public virtual string ScreensaverName { get; set; } = "BaseScreensaver";
public virtual bool ScreensaverContainsFlashingImages { get; set; } = false;
```
{% endcode %}

The two overridable properties mentioned above have been inappropriately declared to be settable, despite them being read-only informational properties. In order to maintain consistency, we've decided to remove the setter from the property so that you can override them only once. This ensures that all the information present in the screensaver instances are correct.

{% hint style="info" %}
You should edit the overridden properties so that they don't expose the setters.
{% endhint %}

#### **Culture management is separate from the language management**

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
// Removed
public bool LangChangeCulture { get; set; }

// Renamed to CurrentCultureName
public string CurrentCultStr { get; set; } = "en-US";
```
{% endcode %}

{% code title="CultureManager.cs" lineNumbers="true" %}
```csharp
// Removed
public static void UpdateCultureDry()
public static void UpdateCulture()
public static CultureInfo[] GetCulturesFromCurrentLang()
public static List<string> GetCultureNamesFromCurrentLang()
public static CultureInfo[]? GetCulturesFromLang(string Language)
public static List<string>? GetCultureNamesFromLang(string Language)

// Renamed to CurrentCulture
public static CultureInfo CurrentCult =>
    new(Config.MainConfig.CurrentCultStr);
```
{% endcode %}

{% code title="LanguageInfo.cs" lineNumbers="true" %}
```csharp
// Removed
public string CultureCode =>
    cultureCode;
public CultureInfo[] Cultures =>
    cultures;
    
// Modified to remove cultureCode
public LanguageInfo(string LangName, string FullLanguageName, bool Transliterable, int Codepage = 65001, string cultureCode = "", string country = "")
public LanguageInfo(string LangName, string FullLanguageName, bool Transliterable, string[]? LanguageToken, string cultureCode = "", string country = "")
```
{% endcode %}

{% code title="LanguageManager.cs" lineNumbers="true" %}
```csharp
// Removed
public static string InferLanguageFromSystem()
```
{% endcode %}

To allow users more flexibility into choosing their own culture that is recognized by the kernel, the above functions that are tagged as removed above are deleted from the public API.

{% hint style="danger" %}
There are no alternatives for this.
{% endhint %}

#### **Removed `WelcomeMessage` from the public API**

{% code title="WelcomeMessage.cs" lineNumbers="true" %}
```csharp
public static class WelcomeMessage
```
{% endcode %}

This class was not meant to be used by the kernel mods in the first place, because it contained code that was utilized by the kernel startup sequence, which would be inappropriate to use once the kernel boots up. We've decided to remove this class from the API to prevent misuse.

{% hint style="danger" %}
There are no alternatives for this.
{% endhint %}

#### **Removed fancy console writers**

```csharp
public static class TextDynamicWriters
public static class TextFancyWriters
public static class TextMiscWriters
```

The above classes have been removed, because Terminaux 7.0 is planned to remove the old-school function-based writers, which were marked as obsolete thanks to the new cyclic writers. Those writers were in use by the above static classes.

{% code title="TextWriters.cs" lineNumbers="true" %}
```csharp
public static void WriteListEntry(string entry, string value, KernelColorType ListKeyColor, KernelColorType ListValueColor, int indent = 0)
public static void WriteList<TKey, TValue>(Dictionary<TKey, TValue> List, KernelColorType ListKeyColor, KernelColorType ListValueColor)
public static void WriteList<T>(IEnumerable<T> List, KernelColorType ListKeyColor, KernelColorType ListValueColor)
```
{% endcode %}

In addition to that, the above functions were removed from the `TextWriters` class for the same reason.

{% hint style="info" %}
Consult the Terminaux documentation for more information on how to use the cyclic writers [here](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-writers/cyclic-writers).
{% endhint %}

#### **`SelectionFunctionType` changes**

When using the above settings entry key, you'll need to provide the fully-qualified type name, not just a short name. This is to avoid ambiguity.

**Merged filesystem operation classes**

{% code title="All operation classes" lineNumbers="true" %}
```csharp
public static class (OperationName)

// Relocated to FilesystemTools partial class
public static partial class FilesystemTools
```
{% endcode %}

To avoid fragmentation in the filesystem tools, such as `Opening`, `Listing`, and `Checking`, we've decided to merge such classes, except those that are not directly related to the filesystem operation, to the `FilesystemTools` partial class in the `Nitrocid.Files` namespace.

{% hint style="info" %}
You'll need to update your using clause to point to `Nitrocid.Files` and to update your references to such classes to point to `FilesystemTools`.
{% endhint %}

#### **`CheckConfigVariables()` simplified for `SMultivar` support**

{% code title="ConfigTools.cs" lineNumbers="true" %}
```csharp
public static Dictionary<string, bool> CheckConfigVariables()
public static Dictionary<string, bool> CheckConfigVariables(string configTypeName)
public static Dictionary<string, bool> CheckConfigVariables(BaseKernelConfig? entries)
public static Dictionary<string, bool> CheckConfigVariables(SettingsEntry[]? entries, BaseKernelConfig? config)
```
{% endcode %}

The above function's return value has changed to `List<bool>`. Consequently, you'll no longer be able to get information about which variable is for which, because we've omitted the configuration names.

{% hint style="info" %}
In the final version of 0.1.2, we promise to restore the original functionality, but it's going to use a tuple instead of a dictionary because of a potential of multiple settings keys, especially the `SMultivar` keys, that can hold the same name in the same configuration entry.
{% endhint %}

#### **Inter-addon and inter-mod communication updated**

We've updated the inter-addon and the inter-mod communication so that you can work with the mods and the addons with more depth. See the changes here.

#### **Added info-based reflection functions**

{% code title="FieldManager.cs" lineNumbers="true" %}
```csharp
// UseGeneral removed
public static object? GetFieldValue(string Variable, Type? VariableType, bool UseGeneral = false)

// Entire function removed
public static FieldInfo? GetFieldGeneral(string Variable)
```
{% endcode %}

{% code title="PropertyManager.cs" lineNumbers="true" %}
```csharp
// UseGeneral removed
public static object? GetPropertyValue(string Variable, Type? VariableType, bool UseGeneral = false)

// Entire function removed
public static PropertyInfo? GetPropertyGeneral(string Variable)
```
{% endcode %}

We've added reflection functions that used the following:

* `MethodBase`: for method reflection
* `FieldInfo`: for field reflection
* `PropertyInfo`: for property reflection

As a consequence, we've removed the `Get*General()` functions due to internal structural changes in regards to the configuration reading mechanism, as well as have changed the signature of the `Get*Value()` functions so that they don't have an optional parameter, `UseGeneral`, anymore.

{% hint style="info" %}
`Get*Value()` functions are already aware of the settings-related properties.
{% endhint %}

#### **Moved `Nitrocid.Modifications` to the `Nitrocid.Extras.Mods` addon**

This affects all the classes except the most essential ones and the inter-mod communication class. They have been moved to this addon, so even the kernel requires the usage of the inter-addon communication in order to be able to utilize mod functions.

This is done to prevent the Lite version of Nitrocid KS from being able to run any mod, provided that the necessary mod code, including the starting functions, have been moved to that addon.

{% hint style="info" %}
You can use the inter-addon communication to be able to interact with this addon, since these classes remain public.
{% endhint %}

#### **`Nitrocid.LocaleGen.Core` removed**

This NuGet package didn't expose any public API since its inception. It was originally meant to be as a plan for 0.1.0.x to consolidate all the LocaleGen projects and their siblings into one, but it seems that it was never done as of the release of the second beta of 0.1.0.

Now, we've completed the work of consolidation, removing `Nitrocid.LocaleGen.Core` in the process, resulting in such NuGet package being deprecated without an alternative. Additionally, all the internal projects and LocaleGen itself have been migrated into one application that is to be included in the main Nitrocid build output, `Nitrocid.Locales`.

**Debug writer changed for CompilerServices attributes**

{% code title="DebugWriter.cs" lineNumbers="true" %}
```csharp
public static void WriteDebugPrivacy(DebugLevel Level, string text, int[] SecureVarIndexes, params object?[]? vars)
public static void WriteDebug(DebugLevel Level, string text, params object?[]? vars)
public static void WriteDebugLogOnly(DebugLevel Level, string text, params object?[]? vars)
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object?[]? vars)
public static void WriteDebugDevicesOnly(DebugLevel Level, string text, bool force, params object?[]? vars)
public static bool WriteDebugDeviceOnly(DebugLevel Level, string text, bool force, RemoteDebugDevice device, params object?[]? vars)
public static void WriteDebugChatsOnly(DebugLevel Level, string text, bool force, params object?[]? vars)
```
{% endcode %}

The debug writer's functions have been edited to include three new arguments before the `vars` parameter. However, the following types were used:

* `memberName`: `string` \[`CallerMemberName` attribute]
* `memberLine`: `int` \[`CallerLineNumber` attribute]
* `memberPath`: `string` \[`CallerFilePath` attribute]

Additionally, the nature of `params` in the last argument, along with the usage of an array of any object (as indicated by `object?[]?`), causes these functions to allow you to supply infinite arguments without having to explicitly create an array.

Because of potential conflicts, we've decided to convert the `vars` argument to a normal parameter with the default value of `null`. This is going to break the build, as you'll have to change how you call the functions.

```csharp
public static void Assert(bool condition, ...)
public static void AssertNot(bool condition, ...)
public static void AssertNull<T>(T value, ...)
public static void AssertNotNull<T>(T value, ...)
public static void AssertFail(string message, ...)
```

This also affects all the above `Assert()` functions found in the `DebugCheck` class.

{% hint style="info" %}
You'll have to change how you call these functions. Don't worry; you'll just have to append the `vars:` prefix and create an array just like any other array that holds your variables for text formatting. For example:

```csharp
DebugWriter.WriteDebug(DebugLevel.I, "Hi, {0}!", vars: ["Nitrocid KS"]);
```
{% endhint %}

#### **Refactored console tools**

{% code title="ConsoleTools.cs" lineNumbers="true" %}
```csharp
public static class ConsoleTools
{
    (...)
    public static void ResetColors(bool useKernelColors = false)
    public static void ResetBackground(bool useKernelColors = false)
    public static void ResetForeground(bool useKernelColors = false)
    (...)
}
```
{% endcode %}

The above functions have been moved to the `KernelColorTools` class. Since those functions were the only functions that were made to the public, with no properties or fields set to public, we've decided to mark the `ConsoleTools` class as internal.

{% hint style="info" %}
You can still use these functions in the `KernelColorTools` class.
{% endhint %}

#### **Automatic update downloads removed**

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
public bool AutoDownloadUpdate { get; set; } = true;
```
{% endcode %}

Since we're working on improvements for Nitrocid KS to ensure that it gets updated seamlessly and only when required, we've decided to stop the automatic update downloads by removing the feature. This ensures that we can provide distraction-free user experience.

{% hint style="danger" %}
It's advisable to stop using this configuration entry.
{% endhint %}

#### Removed the NTFS mitigation for the 2021 corruption

{% code title="FilesystemTools.cs" lineNumbers="true" %}
```csharp
public static void ThrowOnInvalidPath(string? Path)
```
{% endcode %}

When we were working on the 0.0.15.0 version of Nitrocid KS (Kernel Simulator back then), we became aware of the NTFS bug causing Windows 10 systems that didn't have the fix to display the "disk corrupt" message when "accessing" the NTFS bitmap, leading the users into rebooting the PC to check the whole disk. We also became aware of the kernel driver bug that caused a crash of the system with Blue Screen of Death (BSOD) when the system tried to access an arbitrary path. As a response, we've released that version with the fix applied as per commit [aa8250c](https://github.com/Aptivi/Nitrocid/commit/aa8250ce5ab777b467e1b58c596cd761b80ba32e).

However, NuGet back then assumed that the version published contained "malware" that actually checked the path string with `Contains()`. This was the e-mail:

> Package KS 0.0.15 owned by your account was identified as malware and deleted.
>
> _— NuGet team, "Malware detected in a NuGet.org package"_

Our intention was not to inject "malware" into the final distribution, so we'd negotiated with the NuGet team about the clarification of our checking method, and this was their response:

> Both the 0.0.15 version and the 0.0.14.2 versions of your KS package triggered our malware detection/validation. The 0.0.15 version was deleted for this reason (our malware analysis team concluded it was malicious). However, given extra details you provided and this is the second instance of the problem, I have submitted the details you provided to our malware analysis team for further review.
>
> Apologies on the delay but, to be safe, we cannot allow this package to complete validation until there is a conclusive response from our malware analysis team. Our team takes the security of our customers extremely seriously and depend on our partner teams to evaluate packages for malware.
>
> In general, if Windows 10 is identifying a package or package contents as malware as a “false positive”, package consumers will run into the very same problem that you and our malware validation is encountering. Therefore, I believe it is best to work with the malware analysis team to resolve this issue conclusively.
>
> _— NuGet team_

Meanwhile, we'd released the clean version under the 0.0.14.3 version with commit [a8d45c3](https://github.com/Aptivi/Nitrocid/commit/a8d45c32afde41aa2ad04ad84cd96832b6394971). The NuGet team then allowed us to push newer versions of Nitrocid KS with the checking code included.

Fast forward to the present, this check was no longer necessary, because almost all computers were patched, so we've decided to remove the check, this time, at will instead of being forced.

{% hint style="warning" %}
You can still implement this code, referring to [this commit](https://github.com/Aptivi/Nitrocid/commit/5d5e886d552e203b2e06ab39665fd6a03c8f3e8f#diff-8720daddbbf90b90112ada4140838886e36eab7f12688ecdccb8bcc2f4dc5e4b) that caused this breaking change, in your mod. However, because this part of code is licensed with GNU GPL 3.0+, you'll have to credit the whole project by preserving the license header found at the top of the code file of Nitrocid KS.

However, some scanners may still detect your mod as "malware," so we don't recommend re-implementing this function at all.
{% endhint %}

#### Theme preview function simplified

{% code title="ThemePreviewTools.cs" lineNumbers="true" %}
```csharp
public static void PreviewThemeSimple(string theme)
public static void PreviewThemeSimple(ThemeInfo theme)
```
{% endcode %}

As we've implemented the color viewer in Terminaux, we've finally removed the "simple" version of the theme preview and merged its functionality with the normal version.

{% hint style="info" %}
This is a behavioral change.
{% endhint %}

#### Base shell info generic class implemented

{% code title="BaseShellInfo.cs" lineNumbers="true" %}
```csharp
public abstract class BaseShellInfo : IShellInfo
```
{% endcode %}

When you create your own shell info classes to give your shell some important information, such as commands and other info, you had to override the `BaseShell` property so that it returned a new instance of your shell. However, this can be a hassle in certain scenarios.

Starting from Nitrocid KS 0.1.2 and Terminaux 7.0, you'll no longer have to override the BaseShell property because we've implemented a generic version of the above class that takes a type of your shell. For example, if your shell is called `OxygenShell` and your shell info class is called `OxygenShellInfo`, you can just inherit the generic version of the class so that it becomes `BaseShellInfo<OxygenShell>`.

As a result, the following properties are removed from the IShellInfo interface:

{% code title="IShellInfo.cs" lineNumbers="true" %}
```csharp
BaseShell? ShellBase { get; }
PromptPresetBase CurrentPreset { get; }
```
{% endcode %}

{% hint style="info" %}
When inheriting the non-generic base shell class, your shell info class might hold wrong information about your shell, even if your commands are defined. Therefore, you must migrate to the generic version of the class if you want to retain your shell settings.
{% endhint %}
