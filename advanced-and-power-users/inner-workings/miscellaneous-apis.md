---
description: >-
  Other inner workings that don't fit with the inner essentials and might be
  useful for your mods
---

# 🌀 Miscellaneous APIs

In addition to the essential APIs that are provided with the Nitrocid kernel that allow you to make awesome mods ranging from simple ones to the most complicated ones, Nitrocid provides some of the useful APIs that don't fit with the category but can be helpful when developing mods.

The following APIs can be used in your mods:

## Integer tools

The `Reflection` part of the kernel contains a class, `IntegerTools`, that consists of useful integer tools, like converting literal file sizes in bytes to their human formats.

### File size conversion

`SizeString()` extension functions can be used when importing the `Reflection` namespace. This allows you to easily convert the file sizes from bytes to their human-readable format.

You can use these functions, once the above namespace is imported, like this:

<pre class="language-csharp" data-title="MyModFuncs.cs" data-line-numbers><code class="lang-csharp">long bytes = 1024L * 1024 * 1024 * 1024;
string humanized = bytes.SizeString();
<strong>// Value of humanized: 1 TB
</strong></code></pre>

{% hint style="warning" %}
You can't use this function for enormous sizes, like 1 zettabytes, because of the limitation of the long integers. However, you shouldn't worry about this situation, since this is used generally for file sizes, and a single file in the world hasn't reached this size yet.
{% endhint %}

## Time zones

Nitrocid KS provides a built-in timezone API that allows you to get information about a timezone and convert the time to the equivalent time using the specific timezone.

This API is found in the `TimeZones` class.

{% hint style="info" %}
If the kernel-wide time zone is enabled, the current kernel time and date changes, depending on your selected kernel-wide time zone. Otherwise, the kernel uses the operating system time and date.
{% endhint %}

One of the functions that the above class implements is `GetZoneTimeString()` and its sibling functions, `GetZoneTimeTimeString()` and `GetZoneTimeDateString()`.

* The first function returns the full date and time using the specified time zone.
* The second function returns the time using the specified time zone.
* The third function returns the date using the specified time zone.

## Properties and Fields

The `Reflection` part of the Nitrocid API provides you with options to access public properties and fields that are declared in the public classes dynamically.

* `PropertyManager` manages properties, such as getting and setting property values.
* `FieldManager` manages fields, such as getting and setting field values.

