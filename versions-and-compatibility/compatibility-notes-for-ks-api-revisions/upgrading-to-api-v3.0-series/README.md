---
icon: up
description: Follow the compatibility notes when upgrading your mods to API v3.0 series
---

# Upgrading to API v3.0 series

As API v3.0 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

{% hint style="danger" %}
## Critically important notices

When upgrading your mods to API v3.0, consider these:

* Starting from 0.1.0, old configuration styles are no longer supported and are kept in your home directory for reference. The kernel will start from scratch as if you've started it for the first time. Don't worry; all your configuration from 0.0.24.0 are still saved in your home directory. This is because of configuration system changes that happened between 0.0.24.0 and 0.1.0.
* .NET Framework 4.8 is **no longer supported** as of 0.1.0 Beta 1. Please consider using .NET 8.0 instead to continue using Nitrocid KS. This is to improve multi-platform support without having to go to one environment (`dotnetfx` on Windows and `mono` on Linux and macOS) for each platform. This is done starting from API version `3.0.25.310`.
* Starting from API version `3.0.25.123`, the mod versions should satisfy the SemVer v2.0 specification. Mod parsing will fail if an invalid version expression is entered.
* Starting from API version `3.0.25.154`, the mod loader will fail if the mod is not strongly signed using any strong naming key and loading untrusted mods is disabled.
* Starting from API version `3.0.25.361`, mods are no longer organized with mod parts. This feature has been removed and won't be coming back.
* Starting from API version `3.0.25.380`, the root namespace has been changed from KS to Nitrocid. This means that you need to update your mods to point to the newer root namespace.
* Starting from API version, `3.0.25.383`, the mod name and the mod version must be specified, because if they aren't specified, the mod parsing fails.

The explanation about these changes can be found at the bottom of this page.
{% endhint %}

## From 0.0.24 to 0.1.0

This version is a futuristic magic that brings in many feature additions and spectacular improvements in all fields, including cosmetic changes.

{% content-ref url="../../version-release-notes/v0.1.x.x-series.md" %}
[v0.1.x.x-series.md](../../version-release-notes/v0.1.x.x-series.md)
{% endcontent-ref %}

### Detailed important changes

This section explains how to adapt the important changes to your mod code so that it works with 0.1.0 and higher. This highlights the most important changes that we have compiled for you.

#### Old configuration styles

The following configuration files (incomplete list) have been changed entirely from 0.0.24.x to at least 0.1.0 to better fit the requirements of having the clean home directory (i.e. moved from the user profile directory to the local application data directory):

```
d-----          3/5/2024  12:20 PM                KSEvents
d-----          3/5/2024  12:20 PM                KSMods
d-----          3/5/2024  12:20 PM                KSReminders
d-----          3/5/2024  12:20 PM                KSSplashes
-a----          3/5/2024  12:20 PM              0 Aliases.json
-a----          3/5/2024  12:20 PM              0 DebugDeviceNames.json
-a----          3/5/2024  12:20 PM          31318 KernelConfig.json
-a----          3/5/2024  12:20 PM             32 MAL.txt
-a----          3/5/2024  12:20 PM             20 MOTD.txt
-a----          3/5/2024  12:20 PM            176 Users.json
```

After you upgrade Nitrocid KS 0.0.24.x to 0.1.0, running it may yield first-time run wizards, thinking that all your configuration is lost. However, they're not lost, because the old configuration styles will not be deleted by 0.1.0. Unfortunately, the two configuration styles are not compatible with each other, meaning that you'll have to manually replicate the configuration that you had made when you were using 0.0.24.x.

This is intentionally done to make the configuration reader and the writer faster than before due to the usage of the serialization techniques, compared to the old method of manually parsing every single configuration key and installing them to the appropriate variables. The new reader and writer also allows more flexibility due to how they're implemented, causing your mods to be more configurable than before.

{% hint style="info" %}
You can learn more about why we've made these changes, as well as a list of commits that may explain more, [here](from-0.1.0-beta-1-to-0.1.0-beta-2.md#removed-the-field-manager).
{% endhint %}

#### Removal of .NET Framework 4.8 support

After 0.0.24.x, you'll notice that we no longer ship a version that is compatible with the .NET Framework 4.8 that is pre-installed in the latest versions of Windows. This is because we have started using features that are exclusive to the modern .NET, and Nitrocid KS 0.1.0 and above currently uses .NET 8.0 as the minimum version needed to run. As such, we've decided to change the requirements according to this change.

{% hint style="info" %}
Please consider using .NET 8.0 instead to continue using Nitrocid KS. This is to improve multi-platform support without having to go to one environment (`dotnetfx` on Windows and `mono` on Linux and macOS) for each platform.
{% endhint %}

Fortunately, we still maintain the 0.0.24.x version, which still supports .NET Framework 4.8. This version will be supported until the full .NET Framework 4.8 deprecation, which will not happen until further notice.

#### Significant improvements to your mods

Starting from 0.1.0, we've significantly made improvements as to how your mods start. Your mods have become more powerful than before, and we're still working on it to ensure that they get more control over how Nitrocid and its addons work. As part of this significant improvement effort that happened during the entire development cycle of this version, we had to do the following important changes to ensure that your mods have the highest quality possible:

* We have removed organizing multiple mods that have the same name using mod parts, because they were relevant back when mods consisted of just a single source code file (Visual Basic or C#) and large mods would be grouped using multiple source code files that inter-operate with each other. Some versions ago, we had removed source-code-based mods and relied on mod developers to make `.DLL` versions to ensure that they get the most flexibility possible. This feature won't be coming back because of its rigidity. See why [here](from-0.1.0-beta-2-to-0.1.0-beta-3.md#removed-mod-parts).
* All pre-API v3.0 versions of Nitrocid KS, including 0.0.24.x, had `KS` as its root namespace, because the name was Kernel Simulator back then. We have given this application a name, called Nitrocid KS, and the kernel name has been changed to Nitrocid Kernel. As a result, the root namespace has been changed from `KS` to `Nitrocid` to be more consistent with the application branding. Some of the breaking change notes still use the `KS` root namespace for historical reasons and they should not be modified as they list the history of changes that happened between the previous version and the next version. You'll have to update your imports to point to the new root namespace. See why [here](from-0.1.0-beta-3-to-0.1.0-rc.md#changed-the-root-namespace).
* Earlier, we had allowed empty mod names and versions, because, back then, they were relevant in cases which the mod authors have decided not to provide the mod name and the mod version, but still provide the mod name as the file name of the loose source code file. Some versions ago, we had removed source-code-based mods for the first reason mentioned above. As a result, we've mandated the mod name and the mod version so that every mod that don't have their name and/or their version will not be parsed. They'll fail to load. See why [here](from-0.1.0-beta-3-to-0.1.0-rc.md#mandatory-mod-version-and-name-properties).
* Also, we have mandated the mod versioning via the SemVer v2.0 versioning scheme. This is to filter versions that are completely or partially invalid to ensure that only valid versions (revisions or not) are allowed. This is mandatory for mods that target Nitrocid KS 0.1.0 to ensure that the mod authors version their mods properly as all the kernel mods are glorified class libraries.
* Finally, we have made signing your mods using your strong name key mandatory. This is to make sure that your mods have a unique identity and that they are attributed to you. This is also to protect the kernel from rogue and often unsigned kernel mods that may cause problems with the kernel or your computer. Although strong naming is generally just for identity, Nitrocid's mod manager will refuse to load mods that are not strongly named for security.

For instructions on how to strongly name your mods, you can consult the below page to perform this operation.

{% content-ref url="../../../advanced-and-power-users/inner-workings/inner-essentials/assembly-signing.md" %}
[assembly-signing.md](../../../advanced-and-power-users/inner-workings/inner-essentials/assembly-signing.md)
{% endcontent-ref %}

### Other breaking changes

We have highlighted the most important breaking changes for your kernel mods. Now, for the other breaking changes, you'll need to adapt the changed from 0.0.24.x to 0.1.0 using the guides that are explained in the below pages:

{% content-ref url="from-0.0.24.x-to-0.1.0-beta-1.md" %}
[from-0.0.24.x-to-0.1.0-beta-1.md](from-0.0.24.x-to-0.1.0-beta-1.md)
{% endcontent-ref %}

{% content-ref url="from-0.1.0-beta-1-to-0.1.0-beta-2.md" %}
[from-0.1.0-beta-1-to-0.1.0-beta-2.md](from-0.1.0-beta-1-to-0.1.0-beta-2.md)
{% endcontent-ref %}

{% content-ref url="from-0.1.0-beta-2-to-0.1.0-beta-3.md" %}
[from-0.1.0-beta-2-to-0.1.0-beta-3.md](from-0.1.0-beta-2-to-0.1.0-beta-3.md)
{% endcontent-ref %}

{% content-ref url="from-0.1.0-beta-3-to-0.1.0-rc.md" %}
[from-0.1.0-beta-3-to-0.1.0-rc.md](from-0.1.0-beta-3-to-0.1.0-rc.md)
{% endcontent-ref %}

{% content-ref url="from-0.1.0-rc-to-0.1.0-final.md" %}
[from-0.1.0-rc-to-0.1.0-final.md](from-0.1.0-rc-to-0.1.0-final.md)
{% endcontent-ref %}

The below sections specify the post-0.1.0 releases.

## From 0.1.0.0 to 0.1.0.3

Between 0.1.0.0 and 0.1.0.3, we've made the following breaking changes:

### Updated Terminaux to 3.3.0.1

We've updated Terminaux to 3.3.0.1 to fix a bug related to the selection style crashing when pressing ESC. In consequence, because the fix was released after the 3.3.0 release, we had to increase the mod API version to `3.0.25.439`.

You can consult the list of breaking changes that result from upgrading Terminaux 3.2.0 to 3.3.0 by pressing the below button:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v3.0" %}
[API v3.0](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v3.0)
{% endcontent-ref %}

## From 0.1.0 to 0.1.1

This version is another futuristic magic that brings in feature additions and spectacular improvements. This version is built on top of the 0.1.0 codebase to provide you with the most gorgeous features ever introduced.

{% content-ref url="../../version-release-notes/v0.1.x.x-series.md" %}
[v0.1.x.x-series.md](../../version-release-notes/v0.1.x.x-series.md)
{% endcontent-ref %}

### Detailed important changes

This section explains how to adapt the important changes to your mod code so that it works with 0.1.1 and higher. This highlights the most important changes that we have compiled for you.

#### Usage of Terminaux 4.x and VisualCard 1.x

Nitrocid has been updated to use Terminaux 4.x and VisualCard 1.x. This is to bring in tons of amazing new features from both the libraries that aim to provide you with the best user and developer experience. You'll need to consult their own manual page for more information about how to adapt your Nitrocid mods to align with the latest breaking changes. VisualCard's breaking changes page is at the top button, and Terminaux's breaking changes page is at the bottom button.

{% content-ref url="https://app.gitbook.com/s/bEvVwD4FK7bX7p8XtIPH/breaking-changes" %}
[Breaking Changes](https://app.gitbook.com/s/bEvVwD4FK7bX7p8XtIPH/breaking-changes)
{% endcontent-ref %}

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes" %}
[Breaking changes](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes)
{% endcontent-ref %}

#### Color requirement functions condensed

{% code title="ThemeTools.cs" lineNumbers="true" %}
```csharp
public static bool Is255ColorsRequired(string theme)
public static bool Is255ColorsRequired(ThemeInfo theme)
public static bool Is255ColorsRequired(Dictionary<KernelColorType, Color> colors)
public static bool IsTrueColorRequired(string theme)
public static bool IsTrueColorRequired(ThemeInfo theme)
public static bool IsTrueColorRequired(Dictionary<KernelColorType, Color> colors)
```
{% endcode %}

The color requirement functions have been condensed so that it becomes easier to use and to understand. They have been condensed into just one function: `MinimumTypeRequired()`.

{% hint style="info" %}
The `MinimumTypeRequired()` function has been implemented to simplify the color requirement detection functions. The signatures are basically the same, but you need to also provide the color type that you want to check at the end of the function.
{% endhint %}

#### `AlarmEntry` implementation

{% code title="AlarmTools.cs" lineNumbers="true" %}
```csharp
public static KeyValuePair<(string, string), DateTime> GetAlarmFromId(string alarmId)
```
{% endcode %}

To more easily manage the alarm instances, we had to implement the `AlarmEntry` class that contains all the necessary properties for each alarm that your mods can control. In order to implement this class, we had to edit all the dictionaries that represent a list of alarms by name so that we hold just the alarm entry instance.

{% hint style="info" %}
Most of the time, you won't need to make any changes to how you call the functions. You just need to be aware of the fact that `GetAlarmFromId()` now returns a `KeyValuePair<string, AlarmEntry>`.
{% endhint %}

#### Removed references to GRILO

{% code title="KernelPlatform.cs" lineNumbers="true" %}
```csharp
public static bool IsRunningFromGrilo()
```
{% endcode %}

As GRILO is being sunset due to the implementation of the bootloader and the kernel environment management tools to Nitrocid, we've decided to remove everything related to GRILO by removing all the functions that have connections with that application.

{% hint style="danger" %}
We advise you to cease using this function. Your bootable apps now need to reference Nitrocid and become a kernel mod in order to work again as a bootable app.
{% endhint %}

#### Access to the part options

{% code title="CommandArgumentPart.cs" lineNumbers="true" %}
```csharp
public Func<string[], string[]> AutoCompleter { get; private set; }
public bool IsNumeric { get; private set; }
public string[] ExactWording { get; private set; }
```
{% endcode %}

We needed to add support for argument descriptions, which would show up in the command-specific help entry for more clarification. However, this added to the burden of maintaining a larg amount of arguments in the `CommandArgumentPart` constructor. As a result, we had to replace these properties with a single property, `Options`, that grants you easy access to the command argument part options.

{% hint style="info" %}
The constructors are not affected; one of it has been provided an extra optional argument that specifies the unlocalized argument description.
{% endhint %}

#### Base screensaver configuration implementation changed

{% code title="MatrixBleed.cs" lineNumbers="true" %}
```csharp
public static class MatrixBleedSettings
```
{% endcode %}

When the Nitrocid KS settings implementation still relied on manual key access and value casting, such as the usage of the indexer that accessed the settings section and keys, we had to proxy the screensaver settings due to the fact that we didn't have a concrete way of accessing the screensaver settings in a meaningful way.

Historically, going back to 0.0.12.0, it was the first kernel series that has added screensaver configuration in its minimal form, such as allowing true color and 256 color modes. Since then, the release of 0.0.20.0 redefined the configuration in a way that became necessary for us to change the settings handler. We used to proxy the screensaver settings because we were manually creating settings entries and processing them. This proxying came in two forms:

* The first list of an individual screensaver settings list contained only value setting, and this is found in the main configuration instance.
* The second list of an individual screensaver settings list contained value setting properties and value checks as implemented in the same file that implemented that screensaver.

For consistency and ease of maintenance, we've decided to remove this proxying, causing all the value check code to move to the kernel screensaver settings instance.

{% hint style="info" %}
Use the screensaver settings instance directly using the `SaverConfig` property in the `Config` class.
{% endhint %}

#### VSIX analyzers no longer shipped

We're no longer shipping the VSIX version of the Nitrocid analyzers because of low interest. Additionally, this version of the analyzers only worked in the full Visual Studio installation, which is only applicable for Windows systems. Moreover, the Community version of Visual Studio and all the other .NET IDEs, such as Rider, can't use this extension, and will have to rely on the NuGet package for analyzers.

Starting from 0.1.1, we've switched the distribution from VSIX to NuGet to be able to selectively install the analyzer to your project of your choice.

{% hint style="warning" %}
You are required to remove the VSIX version to be able to use the NuGet version of the analyzers, because they conflict with each other.
{% endhint %}

#### Moved JSON tools to Textify

{% code title="JsonTextTools.cs" lineNumbers="true" %}
```csharp
public static class JsonTextTools
```
{% endcode %}

We've moved this class to Textify and made sure that all of the functions that use this class point to the newer `JsonTools` class that Textify provides. This is because we wanted these functions to be independent of Nitrocid so that only grabbing Textify would be enough.

{% hint style="info" %}
Change the function references to point to `JsonTools` instead of `JsonTextTools`.
{% endhint %}

#### Removed a RetroKS path property

{% code title="PathsManagement.cs" lineNumbers="true" %}
```csharp
public static string RetroKSDownloadPath
```
{% endcode %}

We've removed a leftover that was spotted during the analysis of the paths during implementation of the widgets. This property was not removed in the final version of Nitrocid KS 0.1.0, but all the code that refers to the RetroKS project was removed due to the obsolescence.

{% hint style="danger" %}
We advice you to stop using this property.
{% endhint %}

#### Centered writer breaking changes

{% code title="TextFancyWriters.cs" lineNumbers="true" %}
```csharp
public static void WriteCentered(int top, string Text, KernelColorType ColTypes, params object[] Vars)
public static void WriteCentered(int top, string Text, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] Vars)
public static void WriteCentered(string Text, KernelColorType ColTypes, params object[] Vars)
public static void WriteCentered(string Text, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] Vars)
public static void WriteCenteredOneLine(int top, string Text, KernelColorType ColTypes, params object[] Vars)
public static void WriteCenteredOneLine(int top, string Text, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] Vars)
public static void WriteCenteredOneLine(string Text, KernelColorType ColTypes, params object[] Vars)
public static void WriteCenteredOneLine(string Text, KernelColorType colorTypeForeground, KernelColorType colorTypeBackground, params object[] Vars)
```
{% endcode %}

Terminaux 4.2.0 and later have introduced a breaking change that involves how the centered text writers work in terms of passing the parameters to the generator. As part of the widget system introduction, we needed to add the margin system. As a result, you'll notice that all calls to this function with the `Vars` argument will need to be revised.

{% hint style="info" %}
You'll need to rewrite how you call these functions so that you either pass a single object array like this: `Vars: vars`, or specify the margin values. You can always default to zeroes, and then you can pass the variables as if nothing happened.
{% endhint %}

#### Symmetric and asymmetric encoding drivers separated

{% code title="IEncodingDriver.cs" lineNumbers="true" %}
```csharp
bool IsSymmetric { get; }
```
{% endcode %}

{% code title="BaseEncodingDriver.cs" lineNumbers="true" %}
```csharp
public virtual bool IsSymmetric =>
    true;
```
{% endcode %}

In order to make implementation of the encoding drivers easier than before, we had to separate the encoding driver to make two versions: Symmetric and asymmetric. We've preserved the name of the symmetric version, while we've given the asymmetric version a new name: `EncodingAsymmetric`.

{% hint style="info" %}
You should change the driver type to match the symmetry type of your encoding algorithm driver. Either way, you should remove the `IsSymmetric` override. If your driver type is:

* symmetric, you don't need to do anything other than removing the `IsSymmetric` override.
* asymmetric, you need to remove the three overrides (`IsSymmetric`, `Key`, and `Iv`) and change the implementation so that your driver implements `BaseEncodingAsymmetricDriver` and `IEncodingAsymmetricDriver`.
{% endhint %}

#### Removed "HDD Uncleaner"

{% code title="KnownAddons.cs" lineNumbers="true" %}
```csharp
/// <summary>
/// HDD Uncleaner 2015 Legacy addon
/// </summary>
LegacyHddUncleaner,
```
{% endcode %}

We've removed an addon that provided you with an amusement app that simulated how an ancient software of ours, "HDD Cleaner", would run. It was only meant for demonstration purposes.

{% hint style="danger" %}
It's advisable to stop using this enumeration value, but the auto generator may override this enumerator's value with another addon.
{% endhint %}

#### Removed config property wrappers

As seen in [this commit](https://github.com/Aptivi/NitrocidKS/commit/e96c4559cf3b20079fc1f960579738fa81e522fd), we've decided to remove the configuration property wrappers as a result of the improvements that were witnessed in the configuration system during the development of the 0.1.0 version.

{% hint style="danger" %}
It's advised to use the `Config.MainConfig` instance to point to the required configuration properties that have their wrappers deleted.
{% endhint %}

#### Removed time/date corner

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
public bool CornerTimeDate { get; set; }
```
{% endcode %}

{% code title="TimeDateTopRight.cs" lineNumbers="true" %}
```csharp
public static class TimeDateTopRight
```
{% endcode %}

The time/date corner that was initially introduced in the 0.0.4.5 version of Nitrocid KS was considered to be one of the oldest features that stayed. Unfortunately, we had to remove this feature in favor of The Nitrocid Homepage.

{% hint style="danger" %}
It's advisable for you to stop using this feature.
{% endhint %}

## From 0.1.1.0 to 0.1.1.13

Between 0.1.1.0 and 0.1.1.13, we've made the following breaking changes:

### Updated Terminaux to 5.0

We've updated Terminaux to 5.0 to bring improvements. However, this doesn't come without the cost of having to deal with the breaking changes, which, in this case, is many.

You can consult the list of breaking changes that result from upgrading to Terminaux 5.0 by pressing the below button:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v5.0" %}
[API v5.0](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v5.0)
{% endcontent-ref %}

## From 0.1.1.13 to 0.1.2

This version is yet another futuristic magic that brings in feature additions and spectacular improvements. This version is built on top of the 0.1.1 codebase to provide you with the most gorgeous features ever introduced.

{% content-ref url="../../version-release-notes/v0.1.x.x-series.md" %}
[v0.1.x.x-series.md](../../version-release-notes/v0.1.x.x-series.md)
{% endcontent-ref %}

### Updated Terminaux to 6.0

We've updated Terminaux to 6.0 to bring improvements. However, this doesn't come without the cost of having to deal with the breaking changes, which, in this case, is many.

You can consult the list of breaking changes that result from upgrading to Terminaux 6.0 by pressing the below button:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v6.0" %}
[API v6.0](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v6.0)
{% endcontent-ref %}

### Detailed important changes

This section explains how to adapt the important changes to your mod code so that it works with 0.1.2 and higher. This highlights the most important changes that we have compiled for you.

#### Removed modern debug log look

{% code title="KernelMainConfig.cs" lineNumbers="true" %}
```csharp
public bool DebugLegacyLogStyle { get; set; } = true;
```
{% endcode %}

We have removed the modern debug log look introduced in the 0.1.0 series, because although it provided a more comfortable look for log reading, we've considered it as a flawed goal due to problems that may come with it, such as log timing differences.

{% hint style="danger" %}
It's advisable for you to stop using this feature.
{% endhint %}

#### Removed `SplashDisplaysProgress`

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

#### Removed `ConfigCategory`

{% code title="ConfigCategory.cs" lineNumbers="true" %}
```csharp
public enum ConfigCategory
```
{% endcode %}

This enumeration went unused as the 0.1.0 configuration has been remade with speed and serialization in mind. Therefore, it got removed as it's of no use. Also, it's limited to only specifying the categories in the main kernel configuration, none of which apply to other configurations, including the custom configuration instances that your mods may install.

{% hint style="info" %}
A viable alternative, `GetSettingsEntries()`, can be used to get the categories from all configurations.
{% endhint %}

#### Merged `ListLanguages()` and `ListLanguagesWithCountry()` functions

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

#### Aptivestigate is used for debugger and crash handler

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

#### Screensaver properties are get-only

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

#### Culture management is separate from the language management

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

#### Removed `WelcomeMessage` from the public API

{% code title="WelcomeMessage.cs" lineNumbers="true" %}
```csharp
public static class WelcomeMessage
```
{% endcode %}

This class was not meant to be used by the kernel mods in the first place, because it contained code that was utilized by the kernel startup sequence, which would be inappropriate to use once the kernel boots up. We've decided to remove this class from the API to prevent misuse.

{% hint style="danger" %}
There are no alternatives for this.
{% endhint %}

#### Removed fancy console writers

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

#### `SelectionFunctionType` changes

When using the above settings entry key, you'll need to provide the fully-qualified type name, not just a short name. This is to avoid ambiguity.

#### Merged filesystem operation classes

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

#### `CheckConfigVariables()` simplified for `SMultivar` support

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

#### Inter-addon and inter-mod communication updated

We've updated the inter-addon and the inter-mod communication so that you can work with the mods and the addons with more depth. See the changes here.

{% content-ref url="../../../advanced-and-power-users/kernel-modifications/inter-mod-communication.md" %}
[inter-mod-communication.md](../../../advanced-and-power-users/kernel-modifications/inter-mod-communication.md)
{% endcontent-ref %}

{% content-ref url="../../../advanced-and-power-users/kernel-modifications/inter-addon-communication.md" %}
[inter-addon-communication.md](../../../advanced-and-power-users/kernel-modifications/inter-addon-communication.md)
{% endcontent-ref %}

#### Added info-based reflection functions

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

#### Moved `Nitrocid.Modifications` to the `Nitrocid.Extras.Mods` addon

This affects all the classes except the most essential ones and the inter-mod communication class. They have been moved to this addon, so even the kernel requires the usage of the inter-addon communication in order to be able to utilize mod functions.

This is done to prevent the Lite version of Nitrocid KS from being able to run any mod, provided that the necessary mod code, including the starting functions, have been moved to that addon.

{% hint style="info" %}
You can use the [inter-addon communication](../../../advanced-and-power-users/kernel-modifications/inter-addon-communication.md) to be able to interact with this addon, since these classes remain public.
{% endhint %}

#### `Nitrocid.LocaleGen.Core` removed

This NuGet package didn't expose any public API since its inception. It was originally meant to be as a plan for 0.1.0.x to consolidate all the LocaleGen projects and their siblings into one, but it seems that it was never done as of the release of the second beta of 0.1.0.

Now, we've completed the work of consolidation, removing `Nitrocid.LocaleGen.Core` in the process, resulting in such NuGet package being deprecated without an alternative. Additionally, all the internal projects and LocaleGen itself have been migrated into one application that is to be included in the main Nitrocid build output, `Nitrocid.Locales`.

#### Debug writer changed for CompilerServices attributes

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
