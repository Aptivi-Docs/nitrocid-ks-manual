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

## Time tools

Nitrocid KS provides you with various APIs that allow you to manage time and date and their components. Here are the following tools that you can use:

### Time zones

Nitrocid KS provides a built-in timezone API that allows you to get information about a timezone and convert the time to the equivalent time using the specific timezone.

This API is found in the `TimeZones` class.

{% hint style="info" %}
If the kernel-wide time zone is enabled, the current kernel time and date changes, depending on your selected kernel-wide time zone. Otherwise, the kernel uses the operating system time and date.
{% endhint %}

One of the functions that the above class implements is `GetZoneTimeString()` and its sibling functions, `GetZoneTimeTimeString()` and `GetZoneTimeDateString()`.

* The first function returns the full date and time using the specified time zone.
* The second function returns the time using the specified time zone.
* The third function returns the date using the specified time zone.

### Calendar management API

In addition to providing the calendar command in the addon, the base Nitrocid API provides some of the calendar management APIs to make access to them easier than before. You can now get the calendar straight from the calendar type or its name using the `GetCalendar()` function from the `CalendarTools` class.

Additionally, the time and date renderers can be used with the base calendar class instance obtained from the above function.

{% hint style="warning" %}
While the events can be configured to be a yearly event, such as the Nitrocid KS release anniversary, such events have to be created by hand until the event commands are updated.
{% endhint %}

### Date conversion API

Nitrocid API provides date conversion tools that allow you to change how the date and the time are being represented. For instance, you can translate the date and the time to UNIX time and vice versa.

As for the calendars, you can use the `GetDateFromCalendar()` function, provided that you have a calendar instance from the `GetCalendar()` function.

Alternatively, you can use the `GetDateFromCalendarNoCulture()` function for calendars with overridden `Calendar` property.

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

If you want to either plainly write text or with a custom color of your choice, consult the Terminaux guide for more information:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-writers" %}
[Console Writers](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-writers)
{% endcontent-ref %}

## Resetting colors

If you need to reset the colors for further text to be written to the console in its natural colors, you can use the `ResetColors()` function in the `ConsoleTools` class to reset the foreground and the background colors to their defaults.

```csharp
public static void ResetColors(bool useKernelColors = false)
```

Additionally, if you pass `true` to the `useKernelColors` parameter, the colors will be reset to the neutral text color for the foreground color and the kernel background color for the background color.

## Alarms

When it comes to alarms, they are useful to alarm you for something at a specified time. This service and its tools can be accessed via the `AlarmTools` class.

```csharp
public static class AlarmTools
```

You can start an alarm using the `StartAlarm()` function that lets you specify your alarm ID, your alarm name, and your alarm interval in seconds.

```csharp
public static void StartAlarm(string alarmId, string alarmName, int alarmValue)
```

Additionally, you can stop an alarm before it's up using a function defined below:

```csharp
public static void StopAlarm(int alarmIdx)
public static void StopAlarm(string alarmId)
```

## Array tools

The array tools class provides you a wide range of tools for manipulating with arrays, such as array randomization, array sorting, and more.

To randomize arrays, the below two functions that do exactly the same thing under different implementations are available:

* `RandomizeArray()`: Uses the [Schwartzian transform](http://en.wikipedia.org/wiki/Schwartzian\_transform) to randomly sort the array.
* `RandomizeArraySystem()`: Uses the .NET 8.0 [`Shuffle()`](https://learn.microsoft.com/en-us/dotnet/api/system.random.shuffle) function from [`Random`](https://learn.microsoft.com/en-us/dotnet/api/system.random) to randomly sort the array.

You can consult the [Nitrocid API Reference](https://aptivi.github.io/NitrocidKS/api/KS.Misc.Reflection.ArrayTools.html) for more array tools.

## JSON Difference

The JSON difference finding tool can be accessed using the `FindDifferences()` function found in the `JsonTools` class. This allows you to find differences in addition and deletion of any JSON object. The difference tool returns the difference in the following format:

* A JSON object with either a plus (`+`), an asterisk (`*`), or a minus (`-`) sign if the target object is an object.
* A JSON object with either a plus (`+`) or a minus (`-`) sign listing differences in addition and deletion of array elements if the target object is an array.
* A JSON object with a plus (`+`) sign indicating the target object and a minus (`-`) sign indicating the source object.
