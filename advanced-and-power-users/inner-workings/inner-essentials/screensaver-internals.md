---
description: Your mods and your screensavers
---

# 🌃 Screensaver Internals

Since Beta 3, your mods can now control whether to register or to unregister your custom screensaver or not. However, let's explain things one by one to learn more about how your mods can interact with screensavers.

## Kernel Mods and their role

Kernel mods can register their screensaver if they have one or more screensaver classes and have created a new instance of such classes using a function that we'll highlight later. However, before registering and/or unregistering, you may want to check the screensaver for existence.

Screensaver management functions are available on the `ScreensaverManager` class.

### Checking for Existence

```csharp
public static bool IsScreensaverRegistered(string name)
```

This function checks the screensaver name for the following conditions:

* If Nitrocid KS has defined a built-in screensaver by its lowercase name, like if you're checking for "`bloom`," then it returns `true`.
* If Nitrocid KS couldn't find a built-in screensaver by its lowercase name, but could find said screensaver in the custom screensaver list, then it returns `true`.
* If neither list indicate that this screensaver exists, but the requested name was "`random`" with respect to `ShowSavers()` treating it specially, then it returns `true`.
* Otherwise, `false`.

### Registering screensavers

```csharp
public static void RegisterCustomScreensaver(string name, BaseScreensaver screensaver)
```

This function checks to see if the requested screensaver is already registered using the checks mentioned above. If the screensaver is not registered, it will add the screensaver entry containing the name and the base screensaver instance to the list of screensavers.

{% hint style="info" %}
Trying to register a custom screensaver if said screensaver already exists causes an exception to be thrown.
{% endhint %}

### Unregistering screensavers

```csharp
public static void UnregisterCustomScreensaver(string name)
```

This function checks to see if the requested screensaver is is already registered using the checks mentioned above. If the screensaver is registered, it will remove the requested screensaver from the custom screensaver list.

{% hint style="info" %}
Trying to unregister a screensaver that doesn't exist causes an exception to be thrown.
{% endhint %}
