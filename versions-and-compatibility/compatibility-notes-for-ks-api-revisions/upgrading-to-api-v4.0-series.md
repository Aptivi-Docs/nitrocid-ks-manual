---
description: Follow the compatibility notes when upgrading your mods to API v4.0 series
icon: up
---

# Upgrading to API v4.0 series

As API v4.0 is still in development, the breaking changes get committed and land here. They describe what broke and what should be used instead.

## From 0.1.2 to 0.2.0 <a href="#from-0.0.24-to-0.1.0" id="from-0.0.24-to-0.1.0"></a>

This version gives your kernel a minor gorgeous makeover that brings in feature additions and spectacular improvements in all fields, including some of the cosmetic changes.

### Updated Terminaux to 7.0 <a href="#updated-terminaux-to-6.0" id="updated-terminaux-to-6.0"></a>

We've updated Terminaux to 7.0 to bring improvements. However, this doesn't come without the cost of having to deal with the breaking changes, which, in this case, is many.

You can consult the list of breaking changes that result from upgrading to Terminaux 7.0 by pressing the below button:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v7.0" %}
[API v7.0](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/breaking-changes/api-v7.0)
{% endcontent-ref %}

### Detailed important changes <a href="#detailed-important-changes-2" id="detailed-important-changes-2"></a>

This section explains how to adapt the important changes to your mod code so that it works with 0.2.0 and higher. This highlights the most important changes that we have compiled for you.

#### **LanguagePacks addon removed**

The LanguagePacks addon has been removed due to the LocaleStation migration that happened during the Terminaux 7.0 preparation stage as part of the development plans. Terminaux 7.0 Beta 4, which has been scheduled for July 31st, 2025, has incorporated langauge tools according to the tools that LocaleStation provides.

As a result, we've decided to remove the LanguagePacks addon.

#### Condensed the language manager

LocaleStation has been used in the whole Nitrocid kernel. We've condensed the language manager to remove all the following features:

* Custom languages
* Installation and uninstallation of custom languages
* Mod localizations

Mod localizations can be easily dealt with, but only if you've added the custom language action for your mod using the functions that LocaleStation provides.

{% hint style="danger" %}
The inter-addon communication facility will report errors when using one of the following removed functions and properties:

* `ModInfo.ModStrings`
* `ModManager.GetLocalizedText()`
{% endhint %}

As part of the condensation, we've also removed the following:

* `LanguageInfo.Codepage`
* `LanguageInfo.Country`
* `LanguageInfo.Transliterable`
* `LanguageInfo.Custom`
* `public LanguageInfo(string LangName, string FullLanguageName, bool Transliterable, int Codepage = 65001, string country = "")`
* `public LanguageInfo(string LangName, string FullLanguageName, bool Transliterable, string[]? LanguageToken, string country = "")`

#### Moved `KernelMain` to `Nitrocid` for the .Base migration

{% code title="KernelMain.cs" lineNumbers="true" %}
```csharp
public static class KernelMain
```
{% endcode %}

We've recently moved `KernelMain` from `Nitrocid.Kernel` to `Nitrocid` to satisfy the .Base migration more smoothly. This is as part of the API v4.0 version that all mods will have to use.

{% hint style="danger" %}
Due to how `KernelMain` is not migrated to the .Base library, you can no longer use this class. Instead, you'll have to rely on `KernelReleaseInfo` to get the properties that you were using.
{% endhint %}

#### Argument parser code moved to Terminaux 7.0

```csharp
// Nitrocid.Arguments
public abstract class ArgumentExecutor : IArgument
public class ArgumentInfo
public class ArgumentParameters
public static class ArgumentParse
public interface IArgument

// Nitrocid.Arguments.Help
public static class ArgumentHelpPrint
```

The argument parser code has been moved to Terminaux 7.0, because the functions that are inside are application-independent. The arguments themselves haven't been moved because they are specific to Nitrocid.

{% hint style="success" %}
We are working on the documentation of the argument parser in the Terminaux documentation, so be patient.
{% endhint %}

#### Remaining shell code moved to Terminaux 7.0

Features such as UESH scripting and process execution have been moved to Terminaux 7.0's shell implementation to match the Nitrocid one. Furthermore, this movement has resulted in us removing all relevant shell code, except the Nitrocid-specific code.

{% hint style="info" %}
The shell documentation has been moved to Terminaux 7.0. Check it out using the link below:

[Shells](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/shells "mention")
{% endhint %}

#### Removed console driver

{% code title="BaseConsoleDriver.cs" lineNumbers="true" %}
```csharp
public abstract class BaseConsoleDriver : IConsoleDriver
```
{% endcode %}

{% code title="ConsoleDriverTools.cs" lineNumbers="true" %}
```csharp
public static class ConsoleDriverTools
```
{% endcode %}

{% code title="IConsoleDriver.cs" lineNumbers="true" %}
```csharp
public interface IConsoleDriver : IDriver
```
{% endcode %}

{% code title="DriverHandler.cs" lineNumbers="true" %}
```csharp
public static IConsoleDriver CurrentConsoleDriverLocal
public static IConsoleDriver CurrentConsoleDriver
```
{% endcode %}

{% code title="DriverTypes.cs" lineNumbers="true" %}
```csharp
public enum DriverTypes
{
    (...)
    Console,
    (...)
}
```
{% endcode %}

{% code title="KernelDriverConfig.cs" lineNumbers="true" %}
```csharp
public string CurrentConsoleDriver
```
{% endcode %}

The console driver has been removed following Terminaux's addition of the brand new console wrapper that doesn't rely on delegated actions. This was necessary to simplify the console wrapper feature in Terminaux and to have it handle the console driver's features.

{% hint style="info" %}
Consult Terminaux's documentation on how to register and to set the console wrapper.
{% endhint %}

#### Moved theming system to Terminaux

{% code title="Theming system" lineNumbers="true" %}
```csharp
// Nitrocid.ConsoleBase.Colors
public enum KernelColorSetErrorReasons
public static class KernelColorTools
public enum KernelColorType

// Nitrocid.ConsoleBase.Themes
public enum ThemeCategory
public class ThemeInfo
public static class ThemePreviewTools
public enum ThemeSetErrorReasons
public static class ThemeTools
```
{% endcode %}

The theming system that Nitrocid used has been moved to Terminaux to give all other Terminaux applications advantage for using Nitrocid's features. Calls to text writers have also been changed to reflect the appropriate theme to set.

{% hint style="info" %}
Consult Terminaux's documentation on how to use the theming system.
{% endhint %}

#### Theme-based writers moved to Terminaux

{% code title="Text*Writers.cs" lineNumbers="true" %}
```csharp
public static class TextDynamicWriters
public static class TextWriters
```
{% endcode %}

The text writers that use the theme color type have been moved to Terminaux, causing us to remove those two classes entirely. This is a massive change that will mandate the usage of what Terminaux implements due to the way the migration has been done. The relevant functions have been moved to their relevant places, resulting in the `ListWriterColor` being re-introduced.

{% hint style="info" %}
Consult Terminaux's documentation on how to write to the console.
{% endhint %}

#### All Nitrocid functions moved to Nitrocid.Base

The root namespace for all Nitrocid functions has been changed from Nitrocid to Nitrocid.Base to separate the entry point from the actual product code, since the mods use the base library as a dependency 100% of the time. Also, it was considered to be best practice to distribute NuGet packages that result from building libraries and not `.exe` files.

We had planned to do this during very early development of the v0.0.x series, but we didn't do that because we had introduced kernel mods from `.dll` files very late.

{% hint style="info" %}
Update your using clauses to point the root namespace of Nitrocid to Nitrocid.Base.
{% endhint %}

#### Calendar classes moved to Terminaux

{% code title="*Calendar*.cs" lineNumbers="true" %}
```csharp
// Nitrocid.Base.Kernel.Time.Calendars
public abstract class BaseCalendar : ICalendar
public static class CalendarTools
public enum CalendarTypes
public interface ICalendar
```
{% endcode %}

The calendar classes have been moved to Terminaux as we were working on porting the calendar cyclic writer to Terminaux to give the other console applications more features. Events and reminders, however, weren't moved due to them being Nitrocid-specific.

{% hint style="info" %}
Those classes might get moved again to a brand new library released later this year, which will provide more features. In case this happens, we'll update both Terminaux and Nitrocid documentations to point to that library's docs.
{% endhint %}

#### Removed `SplashClosing` from the `ISplash` interface

{% code title="ISplash.cs" lineNumbers="true" %}
```csharp
bool SplashClosing { get; set; }
```
{% endcode %}

{% code title="BaseSplash.cs" lineNumbers="true" %}
```csharp
public virtual bool SplashClosing { get; set; }
```
{% endcode %}

Earlier, we used to allow users to override the `SplashClosing` property that sent signals to the kernel that the splash screen was closing. However, it worked only when the current splash instance declares that it's done.

Unfortunately, when the kernel switches to the normal splash screen as a result of an addon or a mod being unloaded, the kernel didn't realize that the splash screen needed closing, because `SplashClosing` was false for all other splash instances except the addon-supplied one, which is no longer found. As a result, the kernel might hang on a blank screen when trying to restart it.

This was a bad design, so we've fixed it by making the `SplashClosing` property in the base splash class static, while still making it available to the public. The interface definition of the same property has been removed as part of this change. This was important to fix this bug.

{% hint style="info" %}
This bug fix will be integrated to the next Nitrocid v0.1.2.x and v0.1.0.x service pack releases expected at the end of August.
{% endhint %}

{% hint style="danger" %}
Please remove all overrides to this property.
{% endhint %}
