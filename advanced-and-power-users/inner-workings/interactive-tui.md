---
description: Your apps are now interactive
---

# ⌨ Interactive TUI

The interactive TUI allows you to make your apps interactive if they provide one or two data sources, which consist of a list of strings, integers, and even class instances, to make getting information about them easier. The interactive TUI renders the screen in two panes, the top being a status bar, and the bottom being a list of key bindings. For clarification, the `ifm` command uses the double pane interactive TUI and the `taskman` command uses the single pane interactive TUI with info in the second pane:

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Double-paned interactive TUI with the ability to switch between two panes</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption><p>Single-paned interactive TUI</p></figcaption></figure>

{% hint style="info" %}
You can exit out of any interactive TUI application by pressing the `ESC` key on your keyboard.
{% endhint %}

## Can I make one, too?

Yes! You can make your own interactive TUI application. Depending on your requirements, you may want to make a plan as to how would your interactive TUI application be.

For each application, you must make a class that would implement both the `BaseInteractiveTui` class and the `IInteractiveTui` interface, just like below:

{% code title="MyTui.cs" lineNumbers="true" %}
```csharp
internal class MyTui : BaseInteractiveTui, IInteractiveTui
{
    public override List<InteractiveTuiBinding> Bindings { get; set; } = new()
    {
        new InteractiveTuiBinding("Action", ConsoleKey.F1, (data, _) => Proceed(data))
    };

    public override IEnumerable PrimaryDataSource =>
        new string[] { "One", "Two", "Three", "Four" };

    public override void RenderStatus(object item)
    {
        string currentItem = (string)item;
        Status = currentItem;
    }

    public override string GetEntryFromItem(object item)
    {
        string currentItem = (string)item;
        return $" [{currentItem}]";
    }

    private static void Proceed(object data)
    {
        string currentItem = (string)data;
        InfoBoxColor.WriteInfoBox(currentItem);
        RedrawRequired = true;
    }
}
```
{% endcode %}

However, you cannot execute your interactive TUI based on your class unless you use this (assuming that you've already defined a command entry in your mod entry point class called `mycommand`):

{% code title="MyCommand.cs" lineNumbers="true" %}
```csharp
public override void Execute(string StringArgs, string[] ListArgsOnly, string[] ListSwitchesOnly) =>
    InteractiveTuiTools.OpenInteractiveTui(new MyTui());
```
{% endcode %}

If everything goes well, you should see this:

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Your interactive TUI app in action with a single pane</p></figcaption></figure>

And if you press your key binding, you'll get this:

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Your keybinding in action</p></figcaption></figure>

For multiple panes, you'll have to modify your class to take two data sources and adapt it to interact with the second pane, like below: (note the highlighted parts, they are added)

<pre class="language-csharp" data-title="MyTui.cs" data-line-numbers><code class="lang-csharp">internal class MyTui : BaseInteractiveTui, IInteractiveTui
{
    public override List&#x3C;InteractiveTuiBinding> Bindings { get; set; } = new()
    {
<strong>        new InteractiveTuiBinding("Switch", ConsoleKey.Tab, (_, _) => SwitchPanes()),
</strong>        new InteractiveTuiBinding("Action", ConsoleKey.F1, (data, _) => Proceed(data)),
    };

<strong>    public override bool SecondPaneInteractable =>
</strong><strong>        true;
</strong>
    public override IEnumerable PrimaryDataSource =>
        new string[] { "One", "Two", "Three", "Four" };

<strong>    public override IEnumerable SecondaryDataSource =>
</strong><strong>        new string[] { "Five", "Six", "Seven", "Eight", "Nine", "Ten" };
</strong>
    public override void RenderStatus(object item)
    {
        string currentItem = (string)item;
        Status = currentItem;
    }

    public override string GetEntryFromItem(object item)
    {
        string currentItem = (string)item;
        return $" [{currentItem}]";
    }

    private static void Proceed(object data)
    {
        string currentItem = (string)data;
        InfoBoxColor.WriteInfoBox(currentItem);
        RedrawRequired = true;
    }

<strong>    private static void SwitchPanes()
</strong><strong>    {
</strong><strong>        CurrentPane++;
</strong><strong>        if (CurrentPane > 2)
</strong><strong>            CurrentPane = 1;
</strong><strong>        RedrawRequired = true;
</strong><strong>    }
</strong>}
</code></pre>

If everything goes well, you should be able to switch to the second pane, causing you to be able to select items from the second pane:

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Your double-paned TUI app in action</p></figcaption></figure>

And if you try to execute your key binding on an item found in the second pane, you'll see this:

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Your keybinding in action</p></figcaption></figure>

{% hint style="danger" %}
You **must** make a keybinding called `Switch` so that your users can choose items for the second pane in double-paned TUI applications, or they won't be able to switch to the second pane!
{% endhint %}

Additionally, you can make your TUI app refresh every set millisecond so that your app can update itself based on the **selected** data, like weather for the selected city. For this, you need an information source that is dynamic and self-updating (from the `GetInfoFromItem()` function), like stopwatches, random data, or even self-updating data gathered from the Internet, based on the selected item in the first pane, assuming that you know how to process them correctly.

For example, to use the Namer library to make a single-paned TUI application that gathers random names to list 10 names in the info pane, you must add a NuGet package, Namer, to your mod's dependencies. To learn more about how to use this library, consult the below page:

{% content-ref url="http://127.0.0.1:5000/s/gmP2CdmfwirIpCISUoX8/usage/how-to-use" %}
[How to use](http://127.0.0.1:5000/s/gmP2CdmfwirIpCISUoX8/usage/how-to-use)
{% endcontent-ref %}

The code that would do this would look like this:

<pre class="language-csharp" data-title="MyTui.cs" data-line-numbers><code class="lang-csharp">internal class MyTui : BaseInteractiveTui, IInteractiveTui
{
    public override List&#x3C;InteractiveTuiBinding> Bindings { get; set; } = new();

    public override int RefreshInterval => 15000;

    public override IEnumerable PrimaryDataSource =>
        new string[] { "Test" };

    public override void RenderStatus(object item)
    {
        string currentItem = (string)item;
        Status = currentItem;
    }

    public override string GetEntryFromItem(object item)
    {
        string currentItem = (string)item;
        return $" [{currentItem}]";
    }
<strong>    public override string GetInfoFromItem(object item)
</strong><strong>    {
</strong><strong>        var namesBuilder = new StringBuilder();
</strong><strong>
</strong><strong>        var list = NameGenerator.GenerateNames(10);
</strong><strong>        for (int i = 0; i &#x3C; list.Count; i++)
</strong><strong>        {
</strong><strong>            string name = list[i];
</strong><strong>            namesBuilder.AppendLine(name);
</strong><strong>        }
</strong><strong>
</strong><strong>        return namesBuilder.ToString();
</strong><strong>    }
</strong>}
</code></pre>

If everything goes well, you should see your TUI app refresh every 15 seconds:

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption><p>Your timed TUI app in action</p></figcaption></figure>

### Colors for the TUI

You can also specify the colors for your TUI application, too! Currently, your interactive TUI uses the regular colors defined under `InteractiveTuiColors`, which gets its values from the kernel configuration that you can also customize.

However, you can override the TUI colors by using the `new` keyword on all the `*Color` properties to assign it a new `Color` value. For example, the contacts manager gets its own colors from its own colors class, which is also configurable through the kernel settings, like below:

{% code title="ContactsManagerCli.cs" lineNumbers="true" %}
```csharp
public static new Color BackgroundColor => ContactManagerCliColors.ContactsManagerBackgroundColor;
public static new Color ForegroundColor => ContactManagerCliColors.ContactsManagerForegroundColor;
public static new Color PaneBackgroundColor => ContactManagerCliColors.ContactsManagerPaneBackgroundColor;
(...)
```
{% endcode %}