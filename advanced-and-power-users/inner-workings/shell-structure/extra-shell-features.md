---
description: The UESH shell provides more features than you can imagine!
---

# 💠 Extra Shell Features

In addition to all the base shell features that UESH contains, the following extra features can be used within the shell. Currently, the following features are supported:

## Cancellation

You can control whether to allow or not to allow cancellation by using the two functions that do exactly the opposite of each other:

```csharp
// To allow cancellation
CancellationHandlers.AllowCancel()

// To inhibit cancellation
CancellationHandlers.InhibitCancel()
```

{% hint style="info" %}
The `CancellationHandlers` class can be found in the `KS.Shell.ShellBase.Commands` namespace.
{% endhint %}

If you call `InhibitCancel()`, it's no longer possible to use `CTRL + C` to cancel the current command. This is useful if the command is in the middle of an uninterruptible work or is in interaction with a native library.

When you've already inhibited the shell cancellation handler, if you call `AllowCancel`, then you can use `CTRL + C` to cancel the current command.
