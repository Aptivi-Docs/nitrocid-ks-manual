---
description: Splash screens!
icon: droplet
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/splash-internals
---

# Splash Internals

<figure><img src="../../../.gitbook/assets/image (186) (1).png" alt=""><figcaption></figcaption></figure>

Splash screens are usually shown when the kernel reaches to the point that the pre-boot environment is no longer needed. Think of these splash screens as Plymouth splash screens that appear on Debian, or the Windows logo that appears when Windows starts. Nitrocid attempts to simulate the same concept.

***

## <mark style="color:$primary;">Splash Management</mark>

The splash management class contains several useful tools to manage them, like loading custom splashes, unloading them, previewing them, etc.

The splash tools consist of the following classes:

* `SplashManager`: A class that handles splashes
* `SplashReport`: A class that handles reporting splashes

The three commonly used functions are:

<details>

<summary>Registering the splashes</summary>

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void RegisterSplash(SplashInfo splashInfo) { }
```
{% endcode %}

This function registers your splash from the `SplashInfo` instance that you've defined in your mod. This allows your mods that have the load priority set to `Important` to register the splashes before the configuration system loads your config.

{% hint style="info" %}
Since the main kernel configuration file holds the splash info, we suggest that you set your mod loading importance to `Important`.
{% endhint %}

</details>

<details>

<summary>Removing the splashes</summary>

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void UnregisterSplash(string splashName) { }
```
{% endcode %}

This function removes your splash from the list of known splashes. This function takes the name of your custom splash, usually taken from your splash's `SplashInfo` instance.

</details>

<details>

<summary>Checking your splash</summary>

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static bool IsSplashRegistered(string splashName) { }
```
{% endcode %}

This function checks the list of splashes to query the splash name for its existence. If the splash exists, it returns true. Otherwise, false is returned.

</details>

***

## <mark style="color:$primary;">Properties in splashes</mark>

You can override the following properties in your splash class:

<table><thead><tr><th width="185.333251953125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>SplashName</code></td><td>Specifies the splash name (usually the same as the name of the splash class).</td></tr><tr><td><code>RequiresBackground</code></td><td>Specifies whether the background colors need to be enabled or not.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Showing Messages during Kernel Boot</mark>

There are ways to show the messages during kernel boot when splashes are enabled.

{% hint style="warning" %}
In your mod start code, please use one of the following `ReportProgress()` functions to let the splash know that your mod is making progress. Don't call any of the console printing functions, since they don't log and may mess up the splash screen, depending on the splash.
{% endhint %}

<details>

<summary>Reporting progress</summary>

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
public static void ReportProgress(string Text, params object[] Vars) { }
public static void ReportProgress(string Text, int Progress, params object[] Vars) { }
public static void ReportProgress(string Text, int Progress, bool force = false, Exception exception = null, SplashReportSeverity severity = SplashReportSeverity.Info, ISplash splash = null, params object[] Vars) { }
```
{% endcode %}

The above functions let you report progress to the splash displayer when the kernel is booting. These messages are passed to the normal progress writer found in the current splash instance, which decides how to display it.

The splash report severity in the last overload, `SplashReportSeverity`, has the following values:

* `Info`
* `Warning`
* `Error`

{% hint style="info" %}
The first function overload for reporting normal progress doesn't increment the progress; it only reports the message to the splash screen for it to display it or to ignore it, depending on the splash.
{% endhint %}

</details>

<details>

<summary>Reporting warnings</summary>

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
public static void ReportProgressWarning(string Text, params object[] Vars) { }
public static void ReportProgressWarning(string Text, Exception exception, params object[] Vars) { }
public static void ReportProgressWarning(string Text, bool force = false, ISplash splash = null, Exception exception = null, params object[] Vars) { }
```
{% endcode %}

The above functions let you report warnings to the splash displayer when the kernel is booting. These messages are passed to the warning progress writer found in the current splash instance, which decides how to display it.

</details>

<details>

<summary>Reporting errors</summary>

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
public static void ReportProgressError(string Text, params object[] Vars) { }
public static void ReportProgressError(string Text, Exception exception, params object[] Vars) { }
public static void ReportProgressError(string Text, bool force = false, ISplash splash = null, Exception exception = null, params object[] Vars) { }
```
{% endcode %}

The above functions let you report errors to the splash displayer when the kernel is booting. These messages are passed to the error progress writer found in the current splash instance, which decides how to display it.

</details>

<details>

<summary>Resetting progress report</summary>

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
public static void ResetProgressReportArea() { }
public static void ResetProgressReportArea(ISplash splash = null) { }
```
{% endcode %}

The above functions reset the progress report so that it says "Loading," so these functions don't actually clear out the progress report. If you have nothing else to report in the splash, you can use these functions.

</details>

<details>

<summary>Splash contexts</summary>

Splashes also contain a context to tell the splash screen that it's in a specific mode, which is one of the following:

<table><thead><tr><th width="133">Context</th><th>Description</th></tr></thead><tbody><tr><td><code>Showcase</code></td><td>This is used to showcase your splash screen and how well it works. Used by <code>previewsplash</code> for best experience.</td></tr><tr><td><code>StartingUp</code></td><td>Used by the kernel to indicate that the kernel is starting up.</td></tr><tr><td><code>ShuttingDown</code></td><td>Used by the kernel to indicate that the kernel is shutting down.</td></tr><tr><td><code>Rebooting</code></td><td>Used by the kernel to indicate that the kernel is rebooting.</td></tr><tr><td><code>Preboot</code></td><td>Used by the kernel to indicate that the kernel is currently on the pre-boot stage before configuration is loaded.</td></tr></tbody></table>

</details>

<details>

<summary>Important messages</summary>

{% code title="SplashManager.cs" lineNumbers="true" %}
```csharp
public static void BeginSplashOut() { }
public static void BeginSplashOut(SplashContext context) { }
public static void EndSplashOut() { }
public static void EndSplashOut(SplashContext context) { }
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

</details>

***

## <mark style="color:$primary;">Boot log buffers</mark>

The kernel stores a short boot log buffer for each session. You can get the boot log by going to the administrative shell and executing the `bootlog` command.

<figure><img src="../../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

You can also access the `LogBuffer` property in the `SplashReport` class, which is defined like this:

{% code title="SplashReport.cs" lineNumbers="true" %}
```csharp
public static string[] LogBuffer =>
    logBuffer.ToArray();
```
{% endcode %}

{% hint style="info" %}
Even if the splash doesn't display any progress messages, they are still saved to the boot log buffers for reference.
{% endhint %}
