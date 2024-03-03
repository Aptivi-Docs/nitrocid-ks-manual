---
description: >-
  Other inner workings that don't fit with the inner essentials and might be
  useful for your mods
---

# 🌀 Miscellaneous APIs

In addition to the essential APIs that are provided with the Nitrocid kernel that allow you to make awesome mods ranging from simple ones to the most complicated ones, Nitrocid provides some of the useful APIs that don't fit with the category but can be helpful when developing mods.

The following APIs can be used in your mods:

## Integer tools

The `Reflection` part of the kernel contains a class, `IntegerTools`, that consists of useful integer tools from short numbers to 128-bit integer numbers to double-precision numbers, like converting literal file sizes in bytes to their human formats.

In addition to that, we've also placed useful extensions, such as converting the number of all kinds, short or long, to different number bases as strings, such as:

* `ToBinary()`
* `ToOctal()`
* `ToNumber()`
* `ToHex()`

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

## Properties and Fields

The `Reflection` part of the Nitrocid API provides you with options to access public properties and fields that are declared in the public classes dynamically.

* `PropertyManager` manages properties, such as getting and setting property values.
* `FieldManager` manages fields, such as getting and setting field values.

In addition to the functions available in the above two classes, you can get all fields and properties defined in all the kernel types using the following functions:

* `GetAllFields()`
* `GetAllFieldsNoEvaluation()`
* `GetAllProperties()`
* `GetAllPropertiesNoEvaluation()`

## Kernel version information

You can get the kernel version information using the following properties from the `KernelMain` class:

* `Version`: Gets the kernel version without the build specifiers
* `VersionFull`: Gets the kernel version with the build specifiers (essentially the same as the GitHub tag for the release)
* `ApiVersion`: Gets the kernel API version.

## Writing to the console

The `Writers` namespace of the Nitrocid-specific `ConsoleBase` namespace contains the following three writer types:

* `TextWriters`: Provides you with all the normal console writers with kernel color types.
* `TextFancyWriters`: Provides you with all the fancy writers with kernel color types.
* `TextMiscWriters`: Provides you with all the miscellaneous writers with kernel color types.
* `TextDynamicWriters`: Provides you with all the dynamically animated console writers with kernel color types.

If you want to either plainly write text or with a custom color of your choice, consult the Terminaux guide for more information:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-writers" %}
[Console Writers](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-writers)
{% endcontent-ref %}

## Array tools

The array tools class provides you a wide range of tools for manipulating with arrays, such as array randomization, array sorting, and more.

To randomize arrays, the below two functions that do exactly the same thing under different implementations are available:

* `RandomizeArray()`: Uses the [Schwartzian transform](http://en.wikipedia.org/wiki/Schwartzian\_transform) to randomly sort the array.
* `RandomizeArraySystem()`: Uses the .NET 8.0 [`Shuffle()`](https://learn.microsoft.com/en-us/dotnet/api/system.random.shuffle) function from [`Random`](https://learn.microsoft.com/en-us/dotnet/api/system.random) to randomly sort the array.

You can consult the [Nitrocid API Reference](https://aptivi.github.io/NitrocidKS/api/KS.Misc.Reflection.ArrayTools.html) for more array tools.
