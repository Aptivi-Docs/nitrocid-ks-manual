---
description: All of the colors!
icon: swatchbook
---

# Color Internals

<figure><img src="../../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

Nitrocid KS uses Terminaux to manipulate with the colors and configure them for the kernel to use. The kernel employs several of the color types for the kernel components, your addons, or your mods to use when writing text using the Nitrocid's console writer.

Scroll down in this page to learn more about Nitrocid-specific features. For the general color tools, you may consult the Terminaux manual for console colors:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-colors" %}
[Console Colors](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-colors)
{% endcontent-ref %}

Colorimetry is also used for more general color tools, which you can consult here:

{% content-ref url="https://app.gitbook.com/s/BdESDsiuTO9fbDXLJ8HV/usage/color-sequences" %}
[Color Sequences](https://app.gitbook.com/s/BdESDsiuTO9fbDXLJ8HV/usage/color-sequences)
{% endcontent-ref %}

## Color types

Nitrocid KS provides you with the following color types to help you make an inspiring theme with nice colors for each type:

| Type                      | Description                                                 |
| ------------------------- | ----------------------------------------------------------- |
| `ContKernelError`         | Continuable kernel panic text (usually sync'd with Warning) |
| `UncontKernelError`       | Uncontinuable kernel panic text (usually sync'd with Error) |
| `NotificationTitle`       | Notification title text                                     |
| `NotificationDescription` | Notification description text                               |
| `NotificationProgress`    | Notification progress text                                  |
| `NotificationFailure`     | Notification failure text                                   |
| `DevelopmentWarning`      | Development warning text                                    |
| `StageTime`               | Stage time text                                             |
| `LowPriorityBorder`       | Low priority notification border color                      |
| `MediumPriorityBorder`    | Medium priority notification border color                   |
| `HighPriorityBorder`      | High priority notification border color                     |

## Color selector

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

The color selector is an interactive TUI that allows you to seamlessly select your favorite color, while getting information about it in the main screen, such as the converted color models, the color levels, and more.

To get information about how to use it, you can find it in the Terminaux manual page:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/other-input/color-wheel" %}
[Color Wheel](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/other-input/color-wheel)
{% endcontent-ref %}

## Color conversion

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Your theme files can also support any specifier, as long as the specifier is supported by Terminaux. For a quick reminder, Terminaux supports the true-color specifiers, alongside the color name or the color number, if you intend to use another color model to select colors.

The commands provided by the color conversion Extras addon help you convert from a color model, such as RGB, to another color model, such as CMYK.

`KernelColorConversionTools` provides you all possible conversion methods to convert a color model to another color model to generate appropriate color specifiers converted to the target unit to create new `Color` instances for your mod's appearance.

For example, if you have Cyan, Magenta, and Yellow values and you want a hex code of it, you can use one of the following function overloads of `ConvertFromCmykToHex()`:

* `ConvertFromCmykToHex(int C, int M, int Y, int K)`
* `ConvertFromCmykToHex(string CMYKSequence)`
