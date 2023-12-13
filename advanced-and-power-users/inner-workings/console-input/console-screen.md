---
description: Your screen in front of you
---

# 🖥 Console Screen

Nitrocid KS offers the console screen feature, which allows you to define a screen for your interactive console application. This guarantees you a dynamic terminal sequence generation that you can print to the console. Usage of the VT sequences, as seen in the Terminaux manual, can be found here:

{% content-ref url="https://app.gitbook.com/s/NaUWjRlaBR1k5rO42Zy8/usage/how-to-use/vt-sequences" %}
[VT Sequences](https://app.gitbook.com/s/NaUWjRlaBR1k5rO42Zy8/usage/how-to-use/vt-sequences)
{% endcontent-ref %}

## `Screen` Instance

{% hint style="info" %}
The explanation provided here is not exhaustive, but a more detailed explanation can be found in the Terminaux manual here:

[Console Screen](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-screen "mention")
{% endhint %}

You can get started by making a new instance of the `Screen` class and using it to add a new `ScreenPart` instance with its name to make a layer for your rendering sequences. This facilitates buffering the screens to the console.

The screen part instance allows you to add text in different ways:

* `AddText()`: Adds a simple and static text to the buffer
* `AddTextLine()`: Adds a simple and static text to the buffer with the extra new line
* `AddDynamicText()`: This is the key of the Screen feature. It allows you to define a function delegate that generates text dynamically.
* `Position()`: Adds a VT sequence that changes the position. Works for static text addition.
* `LeftPosition()`: Adds a VT sequence that changes the cursor left position. Works for static text addition.
* `TopPosition()`: Adds a VT sequence that changes the cursor top position. Works for static text addition.
* `ForegroundColor()`: Adds a VT sequence that changes the foreground color. Works for static text addition.
* `BackgroundColor()`: Adds a VT sequence that changes the background color. Works for static text addition.
* `ResetColor()`: Adds a VT sequence that resets the colors.
* `Clear()`: Clears the whole buffer.
* `GetBuffer()`: Gets the resulting buffer.

{% hint style="info" %}
`AddDynamicText()` is needed if you want to display anything that changes, including a box that changes when the console is resized.
{% endhint %}

## Screen Management

The screen management tools allow you to manipulate with the screen rendering, such as getting the current screen instance, rendering the current screen once, etc.

* `Render()` renders the current screen.
* `Render(Screen)` renders the specified screen.

{% hint style="info" %}
In the `Render()` functions, you can also tell the renderer to clear the screen by passing true to the optional argument, `clearScreen`.
{% endhint %}

However, for `Render()` to work, you need to add your screen instance to the list of tracked screens in the screen manager. This can be done by calling the `SetCurrent()` function on your screen instance.

When this is done, the screensaver manager and the console resize listener will refresh and redraw your screen, taking new console window dimensions to account. This reaction makes your interactive console applications that use screens responsive to the resize events.

{% hint style="warning" %}
Don't forget to remove your screen from the list of tracked screens once you're done using it. You can call `UnsetCurrent()` to make this happen.

If your application contains a main loop wrapped in a `try` and `catch` block, you must create a `finally` block (if not done) and call `UnsetCurrent()` on your screen instance. It may be necessary to move your screen instance declaration in your code outside the `try` and `catch` block.
{% endhint %}

### An example

The kernel interactive testing system allows you to try the demonstration of this feature out to show you the concept of what happens when you try to resize the console when the kernel tracks your screen instance.

The screen instance in question shows you two rulers:

* A horizontal ruler that shows you the width of the console window
* A vertical ruler that shows you the height of the console window

{% @github-files/github-code-block url="https://github.com/Aptivi/NitrocidKS/blob/main/public/Nitrocid/Kernel/Debugging/Testing/Facades/TestScreen.cs" %}
