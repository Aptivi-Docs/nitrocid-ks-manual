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
