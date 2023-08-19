---
description: Splash screens!
---

# 💦 Splash Internals

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Splash screens are usually shown when the kernel reaches to the point that the pre-boot environment is no longer needed. Think of these splash screens as Plymouth splash screens that appear on Debian, or the Windows logo that appears when Windows starts. Nitrocid attempts to simulate the same concept.

The splash tools consists of the following classes:

* `SplashManager`: A class that handles splashes
* `SplashReport`: A class that handles reporting splashes

## Splash Management

The splash management class contains several useful tools to manage them, like loading custom splashes, unloading them, previewing them, etc. The three commonly used functions are:

### Loading the splashes

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void LoadSplashes()
```
{% endcode %}

This function loads all the splash files found in the custom splashes directory, `KSSplashes`. This will load the splash file, verify that it actually holds a single instance of a splash, and register it to the custom splash list.

### Unloading the splashes

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void UnloadSplashes()
```
{% endcode %}

This function does the reverse of `LoadSplashes()` by unloading all the splashes. This means that this function will unregister any splash found in the custom splashes list.

### Previewing the splashes

```csharp
public static void PreviewSplash()
public static void PreviewSplash(bool SplashOut)
public static void PreviewSplash(string splashName)
public static void PreviewSplash(string splashName, bool splashOut)
public static void PreviewSplash(ISplash splash)
public static void PreviewSplash(ISplash splash, bool splashOut)
```

These functions allow you to preview a specific splash screen either by previewing the current one, the specified splash name, or the specified splash base class instance that implements the ISplash instance. The SplashOut argument indicates whether to test out the `BeginSplashOut()` and `EndSplashOut()` functions.

{% hint style="warning" %}
Unless you know what you're doing, avoid using `OpenSplash()` and `CloseSplash()` to show progress. Instead, use one of the `PreviewSplash()` overloads if possible.
{% endhint %}

## Showing Messages during Kernel Boot

There are ways to show the messages during kernel boot when splashes are enabled.

### Reporting progress

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
static void ReportProgress(string Text, int Progress, params object[] Vars)
static void ReportProgress(string Text, int Progress, bool force = false, ISplash splash = null, params object[] Vars)
```
{% endcode %}

The above functions let you report progress to the splash displayer when the kernel is booting. These messages are passed to the normal progress writer found in the current splash instance, which decides how to display it.

### Reporting warnings

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
static void ReportProgressWarning(string Text, params object[] Vars)
static void ReportProgressWarning(string Text, Exception exception, params object[] Vars)
static void ReportProgressWarning(string Text, bool force = false, ISplash splash = null, Exception exception = null, params object[] Vars)
```
{% endcode %}

The above functions let you report warnings to the splash displayer when the kernel is booting. These messages are passed to the warning progress writer found in the current splash instance, which decides how to display it.

### Reporting errors

```csharp
static void ReportProgressError(string Text, params object[] Vars)
static void ReportProgressError(string Text, Exception exception, params object[] Vars)
static void ReportProgressError(string Text, bool force = false, ISplash splash = null, Exception exception = null, params object[] Vars)
```

The above functions let you report errors to the splash displayer when the kernel is booting. These messages are passed to the error progress writer found in the current splash instance, which decides how to display it.

### Important messages

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void BeginSplashOut()
public static void EndSplashOut()
```
{% endcode %}

If you want to show messages or anything interesting during the kernel boot, you may want to use both the `BeginSplashOut()` and `EndSplashOut()` functions, surrounding both with code to show a message inside. Here's a simple example to show a test message:

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
SplashManager.BeginSplashOut();
InfoBoxColor.WriteInfoBox(Translate.DoTranslation("We've reached {0}%!"), vars: prog);
SplashManager.EndSplashOut();
```
{% endcode %}
