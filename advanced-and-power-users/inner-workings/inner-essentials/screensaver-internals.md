---
description: Your mods and your screensavers
icon: desktop
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/screensaver-internals
---

# Screensaver Internals

<figure><img src="../../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Your mods can now control whether to register or to unregister your custom screensaver or not. However, let's explain things one by one to learn more about how your mods can interact with screensavers.

***

## <mark style="color:$primary;">Kernel Mods and their role</mark>

Kernel mods can register their screensaver if they have one or more screensaver classes and have created a new instance of such classes using a function that we'll highlight later. However, before registering and/or unregistering, you may want to check the screensaver for existence.

<details>

<summary>Checking for screensaver existence</summary>

```csharp
public static bool IsScreensaverRegistered(string name) { }
```

This function checks the screensaver name for the following conditions:

* If Nitrocid KS has defined a built-in screensaver by its lowercase name, like if you're checking for "`bloom`," then it returns `true`.
* If Nitrocid KS couldn't find a built-in screensaver by its lowercase name, but could find said screensaver in the custom screensaver list, then it returns `true`.
* If neither list indicate that this screensaver exists, but the requested name was "`random`" with respect to `ShowSavers()` treating it specially, then it returns `true`.
* Otherwise, `false`.

</details>

<details>

<summary>Registering screensavers</summary>

```csharp
public static void RegisterCustomScreensaver(string name, BaseScreensaver screensaver) { }
```

This function checks to see if the requested screensaver is already registered using the checks mentioned above. If the screensaver is not registered, it will add the screensaver entry containing the name and the base screensaver instance to the list of screensavers.

{% hint style="info" %}
Trying to register a custom screensaver if said screensaver already exists causes an exception to be thrown.
{% endhint %}

</details>

<details>

<summary>Unregistering screensavers</summary>

```csharp
public static void UnregisterCustomScreensaver(string name) { }
```

This function checks to see if the requested screensaver is is already registered using the checks mentioned above. If the screensaver is registered, it will remove the requested screensaver from the custom screensaver list.

{% hint style="info" %}
Trying to unregister a screensaver that doesn't exist causes an exception to be thrown.
{% endhint %}

</details>

***

## <mark style="color:$primary;">Screensaver Management</mark>

The screensaver feature of the kernel features two classes: `ScreensaverManager` and `ScreensaverDisplayer`. The former class, which is considered high-level, handles screensaver management and display, while the latter class handles screensaver displaying to save the screen or to lock the screen using low-level functions, which are only available internally.

`ScreensaverManager` can be found on the API reference documentation, which is found in the bottom of the left pane.

Here are the top three features:

<details>

<summary>Saving your screen</summary>

The screensaver management class contains a function with two overloads dedicated to saving your screen:

{% code title="ScreensaverManager.cs" lineNumbers="true" %}
```csharp
public static void ShowSavers() { }
public static void ShowSavers(string saver) { }
```
{% endcode %}

When this function is called, it first checks to see if the screensaver exists, according to the conditions highlighted in the beginning of the page.

If the provided screensaver is `random`, the screensaver manager will select a random screensaver from the list and show it. Otherwise, it'll check both the built-in screensaver list and the custom screensaver list.

{% hint style="info" %}
This is also triggered by the screensaver timeout handler, which is started when the kernel boots. This handler waits for a specified number of milliseconds until the limit is reached. If there is no interaction with the console, the screensaver will activate.
{% endhint %}

</details>

<details>

<summary>Locking your screen</summary>

{% code title="ScreensaverManager.cs" lineNumbers="true" %}
```csharp
public static void LockScreen() { }
```
{% endcode %}

If you want your mod to lock your screen, call the above function to initiate locking. This function calls `ShowSavers()`, which saves your screen.

Once you press any key, this function checks to see if you have password requirement after locking enabled. If it's enabled, the login handler will check to see if your password is empty. If it's not empty, it'll prompt for your password before unlocking.

#### <mark style="color:$primary;">Lock prevention</mark>

Your mod can prevent screen locking by calling the below function:

{% code title="ScreensaverManager.cs" lineNumbers="true" %}
```csharp
public static void PreventLock() { }
```
{% endcode %}

Once the lock prevention is enabled, the kernel screensaver timeout thread will stop and no screen locking attempt will be made when the timeout reaches. To revert back to the original behavior, you can call the below function:

{% code title="ScreensaverManager.cs" lineNumbers="true" %}
```csharp
public static void AllowLock() { }
```
{% endcode %}

</details>

<details>

<summary>Setting default screensaver</summary>

{% code title="ScreensaverManager.cs" lineNumbers="true" %}
```csharp
public static void SetDefaultScreensaver(string saver) { }
```
{% endcode %}

This function allows your mod to set a default screensaver. Once done, it saves the new screensaver name to the appropriate key, `DefaultSaverName`, in the main configuration instance. As soon as it's saved, the configuration is saved.

</details>

***

## <mark style="color:$primary;">Display Control</mark>

Interactive applications might need to listen to the re-render requests so that they can check to see if they need a re-draw.

<details>

<summary>Force a redraw</summary>

In order to force re-rendering, you can check for the `ScreenRefreshRequired` property in the `ScreensaverManager` class.

For instance, applications that use Nitrocid's Interactive TUI usually respect this request by listening for the refresh request here:

{% code title="InteractiveTuiTools.cs" lineNumbers="true" %}
```csharp
if (ScreensaverManager.ScreenRefreshRequired || BaseInteractiveTui.RedrawRequired)
{
    _refreshSelection = true;
    DebugWriter.WriteDebug(DebugLevel.I, "We're redrawing.");
    KernelColorTools.LoadBack(BaseInteractiveTui.BackgroundColor);
    (...)
}
```
{% endcode %}

{% hint style="warning" %}
This property returns `true` if the screensaver has been entered. However, if you need to get the value of this property, you must do so once, because it gets reset to `false` once it's called.
{% endhint %}

{% hint style="info" %}
This doesn't apply to interactive applications that use the Screen feature as the renderer.
{% endhint %}

</details>

<details>

<summary>Unified delays</summary>

Some screensavers allow you to specify a next draw delay upon completion of the `ScreensaverLogic()` code.

You can enable the generalized delay for all the screensavers that use the `Delay()` function in the `ScreensaverManager` class using the following settings:

<table><thead><tr><th width="229.66668701171875">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>ScreensaverUnifiedDelay</code></td><td>Whether to force all screensavers to delay writing in the specified amount of milliseconds or to let all screensavers decide by themselves.</td></tr><tr><td><code>ScreensaverDelay</code></td><td>How many milliseconds to delay (doesn't apply when unified delay is disabled)?</td></tr></tbody></table>

{% hint style="warning" %}
Screensavers that use `SleepNoBlock()` from `ThreadManager` don't get affected by the unified delay switch.
{% endhint %}

</details>

<details>

<summary>Controlled display</summary>

In screensavers that contain for loops, you can use the `Bailing` property to make the code return immediately. This property turns true if screensaver has been interrupted by any key press, such as <kbd>ENTER</kbd>.

{% code title="BoxStitch.cs" lineNumbers="true" %}
```csharp
while (!box1Done && !box2Done && !box3Done && !box4Done)
{
    if (ScreensaverManager.Bailing)
        return;
    (...)
}
```
{% endcode %}

{% hint style="warning" %}
If you don't include the above conditional, your screensaver might take a long time to exit, depending on the loop. It can also sometimes cause the kernel to get stuck permanently on the screensaver.
{% endhint %}

{% hint style="danger" %}
Never use any of the renderers that internally add to the existing screen instance, especially when it comes to infoboxes, in the screensaver code; this exposes whatever was on the screen, and it poses security and privacy risks.
{% endhint %}

</details>

***

## <mark style="color:$primary;">Ambient sound effects</mark>

The screensaver manager handles the ambient sound effects when this feature is turned on from the main kernel configuration. The sound effects will be played on a loop during the screensaver runtime, until you exit the screensaver using either your mouse or your keyboard.

You can control the intensity of the ambient sound effects using the `AmbientSoundFxIntensity` property in the kernel main configuration class, which takes the following values in the `AmbienceFxIntensity` enum:

<table><thead><tr><th width="109.333251953125">Intensity</th><th>Description</th></tr></thead><tbody><tr><td><code>Calm</code></td><td>equivalent to <code>AudioCueType.AmbienceIdle</code></td></tr><tr><td><code>Normal</code></td><td>equivalent to <code>AudioCueType.AlarmIdle</code></td></tr><tr><td><code>Medium</code></td><td>equivalent to <code>AudioCueType.Ambience</code></td></tr><tr><td><code>Intense</code></td><td>equivalent to <code>AudioCueType.Alarm</code></td></tr></tbody></table>

{% hint style="info" %}
In the `AudioCuesTools` class, you can convert the `AmbienceFxIntensity` enum from/to the `AudioCueType` enum.
{% endhint %}
