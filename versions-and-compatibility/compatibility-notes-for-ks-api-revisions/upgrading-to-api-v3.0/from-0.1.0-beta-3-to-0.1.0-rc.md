---
description: Guide for upgrading 0.1.0 Beta 3 mods to 0.1.0 RC
---

# ⬆ From 0.1.0 Beta 3 to 0.1.0 RC

This page lists all the changes that have been made from 0.1.0 Beta 3 to 0.1.0 RC. For upgrading your mods from 0.0.24.x directly to the 0.1.0 series, use the main upgrade page instead.

### Removed "mod part" leftovers

{% code title="IMod.cs" lineNumbers="true" %}
```csharp
/// <summary>
/// Name of part of mod
/// </summary>
string ModPart { get; set; }
```
{% endcode %}

When we removed the mod management code related to mod parts, there were leftovers to that deprecated feature, and none of the mod management parts seem to be using the mod parts feature after its removal on Beta 3.

So, we've decided to ease the task on the mod developers by removing the mod part leftovers, essentially removing the `ModPart` variable that you have to override.

{% hint style="danger" %}
You can no longer use this function as of 0.1.0 Release Candidate.
{% endhint %}

### Changed the root namespace

{% code title="All code files" lineNumbers="true" %}
```csharp
namespace KS.(...)
{
    (...)
}
```
{% endcode %}

The root namespace of NItrocid KS has been finally changed to `Nitrocid` from the abbreviation of the older name, Kernel Simulator (`KS`), to achieve consistency across the whole set of projects, especially Nitrocid's addons that use the newer `Nitrocid` namespace over the older one, `KS`.

As a result, all mods will break due to the change to the root namespace.

{% hint style="info" %}
The root namespace has been changed from KS to Nitrocid, so you need to update all your usings clause to point to the new root namespace. For example, if you're referring to `KS.ConsoleBase`, you need to update it to point to `Nitrocid.ConsoleBase`.
{% endhint %}

### Custom splashes folder removed

{% code title="PathsManagement.cs" lineNumbers="true" %}
```csharp
public static string CustomSplashesPath
```
{% endcode %}

To accommodate the usage of the mod importance, we've removed the custom splashes folder path from the kernel paths. This is because we've added the registration and the unregistration of the custom splashes, which further simplifies the complexity of the custom splashes.

This simplification is going to be pointed out in a separate breaking change section.

{% hint style="info" %}
Your custom splashes are now found in the `KSMods` folder instead of the `KSSplashes` folder.
{% endhint %}

### Changed the splashes model to (un)registration model

```csharp
// Modified
public static List<string> GetNamesOfSplashes()

// Removed
public static void LoadSplashes()
public static void UnloadSplashes()
public static ISplash GetSplashInstance(Assembly Assembly)
```

We've changed the splash loading form to use the registration and the unregistration model. This allows your splashes to be registered in the easiest method possible.

Furthermore, `GetNamesOfSplashes()` has been changed to return an array of strings containing the names of both the base and the custom splashes, making it read-only.

As a result, the removed APIs that are mentioned in the above code block have been removed to respect the changes made to the splash loading system.

{% hint style="info" %}
Your mod should set the importance priority (`LoadPriority`) to `Important` to be able to load the splashes early before configuration parsing takes place.
{% endhint %}

### Mandatory mod version and name properties

{% code title="IMod.cs" lineNumbers="true" %}
```csharp
string Name { get; set; }
string Version { get; set; }
```
{% endcode %}

Earlier, the mods can specify empty version and empty name so that they can have mod file name as the mod name. Now, we've made these properties mandatory so that they can no longer be optional.

Furthermore, we've changed the two properties to be read-only to avoid name and version manipulation.

{% hint style="info" %}
You need to specify a valid SemVer 2.0 compliant version for your mod and your mod name in order to get loaded.
{% endhint %}

### Merged text tools to Textify

This merger contains two changes: removals and migrations.

#### Removals

{% code title="Removed classes and enums" lineNumbers="true" %}
```csharp
public static class CharManager
public static class TextTools
public enum EnclosedDoubleQuotesType
```
{% endcode %}

We've removed these two classes to avoid duplicate code that already exists in Textify for consistency.

#### Migrations

{% code title="Minified classes" lineNumbers="true" %}
```csharp
public static class FigletTools
public static class JsonTools
```
{% endcode %}

We've also minified the two above classes to their absolute minimum to only include properties and functions that are specific to Nitrocid KS.
