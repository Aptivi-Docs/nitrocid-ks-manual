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
