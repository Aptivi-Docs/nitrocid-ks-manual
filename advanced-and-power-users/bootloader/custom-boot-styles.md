---
description: Make your own custom boot style!
icon: boot-heeled
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/bootloader/custom-boot-styles
---

# Custom Boot Styles

When Nitrocid reads the configuration file, the bootloader parses the boot style name and attempts to load that style. Your mods can load custom boot styles by consulting functions in the `BootStyleManager` class that allows you to add your own custom boot style to the bootloader.

***

## <mark style="color:$primary;">Implementing your style</mark>

To implement your custom boot style, these steps must be followed:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Create a boot style class</mark>

Assuming that you have your mod's source code, create a class and name it after your boot style that you want.

Afterwards, write next to the class file `: BaseBootStyle, IBootStyle` and import the required namespace by `using Nitrocid.Kernel.Starting.Bootloader.Style;`.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Override the necessary methods</mark>

Override the necessary methods using the `override` keyword for each one as appropriate.

* `public override Dictionary<ConsoleKeyInfo, Action<BootAppInfo>> CustomKeys { get; }`
* `public override string Render()`
* `public override string RenderHighlight(int chosenBootEntry)`
* `public override string RenderModalDialog(string content)`
* `public override string RenderBootingMessage(string chosenBootName)`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Implement your environment</mark>

Now, implement everything as you wish. Once you're done, add necessary functions in the mod initialization phase to add your own custom boot style.
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Build and install your mod</mark>

Click on the Build menu and select Build Solution. Then, repeat the steps to install your mod as highlighted in [this page](../kernel-modifications/#building).
{% endstep %}
{% endstepper %}

***

## <mark style="color:$primary;">Key handling</mark>

Your custom boot style can make use of the custom key bindings to do custom actions. They can be defined by overriding the `CustomKeys` dictionary with a new dictionary containing the console key and the action with the boot app info passed to it as an argument, like below:

```csharp
public override Dictionary<ConsoleKeyInfo, Action<BootAppInfo>> CustomKeys { get; } = new()
{
    { new ConsoleKeyInfo(...), (bai) => ... }
}
```

If any key other than the `UP ARROW`, `DOWN ARROW`, and `ENTER` is pressed, the key handler attempts to parse the key according to the custom key list defined by your boot style.

If the key pressed is the same as one of the defined keys, the handler executes the action with the chosen boot application, whose type is `BootAppInfo`, as the argument passed to it.

***

## <mark style="color:$primary;">Bootloader state</mark>

You can also access the bootloader state by referencing the `BootloaderState` class. This class provides you with the following options:

* `WaitingForBootKey`
* `WaitingForFirstBootKey`

This can be used for your custom boot styles to change their behavior, depending on the state.
