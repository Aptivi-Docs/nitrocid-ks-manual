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

## Wrapping

As indicated earlier in the command information page, if you enable the wrapping ability in the command flags (`CommandFlags.Wrappable`) for your command, you can use the `wrap` command against your command to be able to see the details of the output of the command without having to scroll (as in Windows).

For example, `jsonbeautify` has been defined with the wrappable flag so that you can use the `wrap` command with it.

```csharp
{ "jsonbeautify",
    new CommandInfo("jsonbeautify", /* Localizable */ "Beautifies the JSON file",
        [
            new CommandArgumentInfo(
            [
                new CommandArgumentPart(true, "jsonfile"),
                new CommandArgumentPart(true, "output"),
            ], [], true)
        ], new JsonBeautifyCommand(), CommandFlags.RedirectionSupported | CommandFlags.Wrappable)
},
```

If your entire screen has been filled and the output isn't done yet, you can use the following controls to be able to control the position:

| Key       | Action                               |
| --------- | ------------------------------------ |
| `Escape`  | Bails from the wrapped output viewer |
| `Page Up` | Scrolls to the previous page         |
| `Home`    | Scrolls to the first page            |
| `End`     | Scrolls to the last page             |
| `Any key` | Scrolls to the next page             |
