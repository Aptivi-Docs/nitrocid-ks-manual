---
description: What are the widgets?
icon: calendar-range
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/widgets
---

# Widgets

<figure><img src="../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Widgets are information containers that give you quick insights about different information, including the world clock and the news, in a full-screen format. These widgets can be found in the modern logon screen and in The Nitrocid Homepage, and you can easily switch between the main screen and the widget pages.

{% hint style="warning" %}
Widgets are not supported in the classic lock screen style and in the custom lock screen styles.
{% endhint %}

***

## <mark style="color:$primary;">Available widgets</mark>

The following widgets are available:

<table><thead><tr><th width="178.66668701171875">Widget</th><th>Description</th></tr></thead><tbody><tr><td><code>AnalogClock</code></td><td>Shows you the analog clock</td></tr><tr><td><code>DigitalClock</code></td><td>Shows you the digital clock</td></tr><tr><td><code>Emoji</code></td><td>Shows you an emoji icon</td></tr><tr><td><code>NotificationIcons</code></td><td>Shows you a group of notifications grouped as icons</td></tr><tr><td><code>NotificationList</code></td><td>Shows you a group of notifications as cards</td></tr><tr><td><code>Photo</code></td><td>Shows you a photo rendered to the console</td></tr><tr><td><code>TextWidget</code></td><td>Shows you text</td></tr></tbody></table>

***

## <mark style="color:$primary;">Setting and configuring widgets</mark>

The `WidgetTools` class provides a plethora of functions that allow you to manipulate with the widgets, such as registering them and unregistering them. You can also get a widget instance and its name.

You can configure the widgets using the settings application by executing the `settings` command, passing it the `-widgets` switch. Select a widget using the up/down arrow keys, then use the tab key to change the focus to the widget settings entry list. You can use the enter key afterwards to customize the widgets.

***

## <mark style="color:$primary;">Building widgets</mark>

In order to be able to build your widget, you must make a kernel mod that will register your widget when it starts (`AddWidget()`) and will unregister it when your mod stops (`RemoveWidget()`). Follow the instructions on how to build your mod [here](../../../advanced-and-power-users/kernel-modifications/your-mod.md) and use it as a starting point to be able to build such a mod.

Afterwards, make a new class file somewhere on your mod source that will hold all your widget code, such as `MyWidget`, and make it implement both the `BaseWidget` class and the `IWidget` interface so that Nitrocid recognizes it as a widget.

<details>

<summary>Example of a widget</summary>

A minimal example for this class can be consulted below:

{% code title="MyWidget.cs" lineNumbers="true" expandable="true" %}
```csharp
using Nitrocid.Users.Login.Widgets;

namespace MyMod
{
    internal class MyWidget : BaseWidget, IWidget
    {
        public override string Cleanup(int left, int top, int width, int height)
        {
            // Your cleanup code here
        }
        
        public override string Initialize(int left, int top, int width, int height)
        {
            // Your initialization code here
        }
        
        public override string Render(int left, int top, int width, int height)
        {
            // Your widget rendering code here
        }
    }
}
```
{% endcode %}

</details>

{% hint style="info" %}
The strings that the three functions return will be printed raw to the console by Nitrocid using the available Terminaux functions, so make sure that you use the `Render` variants of the writers.

In case of things, such as steps, image numbers, or changing colors, you can make use of the class-wide global settings and initialize their initial values by putting the assignments to the Initialize function.

For example, [here](https://github.com/Aptivi/NitrocidKS/blob/main/public/Nitrocid/Users/Login/Widgets/Implementations/AnalogClock.cs) is the implementation of the analog clock widget.

You can also omit the initialization and the clean-up code by making them return an empty string.
{% endhint %}

***

## <mark style="color:$primary;">Widget Canvas</mark>

Widget Canvas API supports both the modern logon screen and the homepage so they extend to pages of widgets. In order to learn more about how widget canvas work, please refer to the below page:

{% content-ref url="widget-canvas.md" %}
[widget-canvas.md](widget-canvas.md)
{% endcontent-ref %}
