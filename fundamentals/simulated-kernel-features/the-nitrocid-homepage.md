---
description: Your homepage, your way!
icon: house
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/the-nitrocid-homepage
---

# The Nitrocid Homepage

<figure><img src="../../.gitbook/assets/image (188) (1).png" alt=""><figcaption></figcaption></figure>

Nitrocid KS introduces you with an awesome homepage that gets started every time you log in, though you can disable it through the kernel settings. It provides you with the following elements:

* Extensible application list
* Settings and About buttons
* A customizable widget that you can turn off and on through the kernel settings
* Top three RSS feeds (you can turn it off and on through the kernel settings)
* Keybindings that allow you to control the homepage

{% hint style="info" %}
In order to show the top three RSS feeds, an RSS kernel addon must be installed, the "Headlines on login" configuration must be enabled, and the kernel must be connected to the Internet.
{% endhint %}

***

## <mark style="color:$primary;">Keybindings</mark>

You can navigate the application list using either the up/down arrow keys, page up/page down arrow keys, or home/end keys. You can also use your mouse to navigate the homepage, but you must enable the mouse support in order to be able to select an item using just your mouse.

The keybindings shown at the bottom of the screen allow you to perform various operations, such as exiting to the shell, logging out, and executing a selected action.

***

## <mark style="color:$primary;">Custom applications</mark>

Your mods can extend the application list so that your homepage becomes more useful. You can use the functions that are made available in the `HomepageTools` class under the `Nitrocid.Shell.Homepage` namespace.

* You can easily register your action by passing in both the application name and your function delegate to the `RegisterAction()` function.
* To unregister the action, you can use the `UnregisterAction()` function, supplying it the name of your custom action that you want to remove.

{% hint style="warning" %}
You must check to see if the action is registered or not using the `IsHomepageActionRegistered()` function, passing it the same name that you want to register. Attempting to register or unregister the action again causes the exception to be thrown with the type of `KernelExceptionType.Homepage`.
{% endhint %}

<details>

<summary>Example of action registration and unregistration</summary>

This is an example that shows you how to register and unregister your action in your mod code, assuming that you have a function that opens a game called Rush:

{% code title="RushModEntry.cs" lineNumbers="true" %}
```csharp
// Register
HomepageTools.RegisterAction("Rush", RushGame.Start);

// Unregister
HomepageTools.UnregisterAction("Rush");
```
{% endcode %}

</details>
