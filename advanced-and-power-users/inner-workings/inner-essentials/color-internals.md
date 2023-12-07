---
description: All of the colors!
---

# ⛱ Color Internals

Nitrocid KS uses Terminaux to manipulate with the colors and configure them for the kernel to use. The kernel employs several of the color types for the kernel components, your addons, or your mods to use when writing text using the Nitrocid's console writer.

The `ConsoleBase` namespace contains a namespace dedicated to color management called Colors that contains a plenty of useful tools for color manipulation. Currently, it contains the following classes:

* `ColorSelector`
* `KernelColorConversionTools`
* `KernelColorTools`

It also contains the following enumerations for different tools:

* `KernelColorSetErrorReasons`
* `KernelColorType`

Scroll down in this page to get started with the list of amazing color tools.

## Color types

Nitrocid KS provides you with the following color types to help you make an inspiring theme with nice colors for each type:

| Type                       | Description                                                 |
| -------------------------- | ----------------------------------------------------------- |
| `Input`                    | Input text                                                  |
| `License`                  | License color                                               |
| `ContKernelError`          | Continuable kernel panic text (usually sync'd with Warning) |
| `UncontKernelError`        | Uncontinuable kernel panic text (usually sync'd with Error) |
| `HostNameShell`            | Host name color                                             |
| `UserNameShell`            | User name color                                             |
| `Background`               | Background color                                            |
| `NeutralText`              | Neutral text (for general purposes)                         |
| `ListEntry`                | List entry text                                             |
| `ListValue`                | List value text                                             |
| `Stage`                    | Stage text                                                  |
| `Error`                    | Error text                                                  |
| `Warning`                  | Warning text                                                |
| `Option`                   | Option text                                                 |
| `Banner`                   | Banner text                                                 |
| `NotificationTitle`        | Notification title text                                     |
| `NotificationDescription`  | Notification description text                               |
| `NotificationProgress`     | Notification progress text                                  |
| `NotificationFailure`      | Notification failure text                                   |
| `Question`                 | Question text                                               |
| `Success`                  | Success text                                                |
| `UserDollar`               | User dollar sign on shell text                              |
| `Tip`                      | Tip text                                                    |
| `SeparatorText`            | Separator text                                              |
| `Separator`                | Separator color                                             |
| `ListTitle`                | List title text                                             |
| `DevelopmentWarning`       | Development warning text                                    |
| `StageTime`                | Stage time text                                             |
| `Progress`                 | General progress text                                       |
| `BackOption`               | Back option text                                            |
| `LowPriorityBorder`        | Low priority notification border color                      |
| `MediumPriorityBorder`     | Medium priority notification border color                   |
| `HighPriorityBorder`       | High priority notification border color                     |
| `TableSeparator`           | Table separator                                             |
| `TableHeader`              | Table header                                                |
| `TableValue`               | Table value                                                 |
| `SelectedOption`           | Selected option                                             |
| `AlternativeOption`        | Alternative option                                          |
| `WeekendDay`               | Weekend day                                                 |
| `EventDay`                 | Event day                                                   |
| `TableTitle`               | Table title                                                 |
| `TodayDay`                 | Today                                                       |
| `TuiBackground`            | Interactive TUI background color                            |
| `TuiForeground`            | Interactive TUI foreground color                            |
| `TuiPaneBackground`        | Interactive TUI pane background color                       |
| `TuiPaneSeparator`         | Interactive TUI pane separator color                        |
| `TuiPaneSelectedSeparator` | Interactive TUI pane selected separator color               |
| `TuiPaneSelectedItemFore`  | Interactive TUI pane selected item color (foreground)       |
| `TuiPaneSelectedItemBack`  | Interactive TUI pane selected item color (background)       |
| `TuiPaneItemFore`          | Interactive TUI pane item color (foreground)                |
| `TuiPaneItemBack`          | Interactive TUI pane item color (background)                |
| `TuiOptionBackground`      | Interactive TUI option background color                     |
| `TuiKeyBindingOption`      | Interactive TUI key binding in option color                 |
| `TuiOptionForeground`      | Interactive TUI option foreground color                     |
| `TuiBoxBackground`         | Interactive TUI box background color                        |
| `TuiBoxForeground`         | Interactive TUI box foreground color                        |

## Color selector

The color selector is an interactive TUI that allows you to seamlessly select your favorite color, while getting information about it in the main screen, such as the converted color models, the color levels, and more.

To get information about how to use it, you can find it in the Terminaux manual page:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/color-wheel" %}
[Color Wheel](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/color-wheel)
{% endcontent-ref %}

## Color conversion

Your theme files can also support any specifier, as long as the specifier is supported by Terminaux. For a quick reminder, Terminaux supports the three true-color specifiers, alongside the color name or the color number, if you intend to use another color model to select colors:

* RGB: Red, Green, and Blue.
  * `<RRR>;<GGG>;<BBB>`
  * where the three variables can be from 0 to 255.
* RYB: Red, Yellow, and Blue.
  * `ryb:<RRR>;<YYY>;<BBB>`
  * where the three variables can be from 0 to 255.
* CMYK: Cyan, Magenta, and Yellow with the Black Key.
  * `cmyk:<CCC>;<MMM>;<YYY>;<KKK>`
  * where these variables can be from 0 to 100.
* CMY: Cyan, Magenta, and Yellow.
  * `cmy:<CCC>;<MMM>;<YYY>`
  * where these variables can be from 0 to 100.
* HSL: Hue, Saturation, and Luminance (or Lightness).
  * `hsl:<HHH>;<SSS>;<LLL>`
  * where the Hue can be from 0 to 360 _**degrees**_ and _**not radians**_.
  * where the Saturation and the Luminance can be from 0 to 100.
* HSV: Hue, Saturation, and Value.
  * `hsv:<HHH>;<SSS>;<VVV>`
  * where the Hue can be from 0 to 360 _**degrees**_ and _**not radians**_.
  * where the Saturation and the Luminance can be from 0 to 100.

The commands provided by the color conversion Extras addon help you convert from a color model, such as RGB, to another color model, such as CMYK.

`KernelColorConversionTools` provides you all possible conversion methods to convert a color model to another color model to generate appropriate color specifiers converted to the target unit to create new `Color` instances for your mod's appearance.

For example, if you have Cyan, Magenta, and Yellow values and you want a hex code of it, you can use one of the following function overloads of `ConvertFromCmykToHex()`:

* `ConvertFromCmykToHex(int C, int M, int Y, int K)`
* `ConvertFromCmykToHex(string CMYKSequence)`

## Color tools

Nitrocid KS provides you a built-in color tools class that allows you to manipulate with the colors in various ways. The following types of manipulation are available:

### Populating a list of colors

You can get a list of colors with all the kernel color types by using one of the three functions, depending on the type of the population:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static Dictionary<KernelColorType, Color> PopulateColorsEmpty()
public static Dictionary<KernelColorType, Color> PopulateColorsDefault()
public static Dictionary<KernelColorType, Color> PopulateColorsCurrent()
```
{% endcode %}

Here's an overview of each function:

* The first function, `PopulateColorsEmpty()`, populates all the colors for all the kernel color types with the black color for all foreground colors and white for background colors.
* The second function, `PopulateColorsDefault()`, populates all the colors for all the kernel color types with the default kernel colors for all the colors, regardless of the kernel configuration.
* The second function, `PopulateColorsCurrent()`, populates all the colors for all the kernel color types with the current kernel colors according to the kernel configuration.

### Getting and Setting colors

In addition to the above function, you can also get a color instance from a single color type and set a color for a specified type to your own selected color. These two functions help you do these two tasks simply:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static Color GetColor(KernelColorType type)
public static Color SetColor(KernelColorType type, Color color)
```
{% endcode %}

{% hint style="info" %}
Any changes made to a kernel color type will be saved to the kernel settings upon shutting the kernel down or rebooting it.
{% endhint %}

### Loading a background color

You can clear the console screen with a specified background color by calling this below function, provided that it contains several versions of the function:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static void LoadBack()
public static void LoadBack(Color ColorSequence)
```
{% endcode %}

There are two versions of this function:

* The first parameterless function allows you to clear the console screen with the current kernel background color.
* The second function with the color parameter allows you to clear the console screen with the selected background color.

### Getting a gray color

You can get a gray foreground color that adapts to the lightness of the background color using a single function, `GetGray()`.

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static Color GetGray()
```
{% endcode %}

This will return either a gray color on dark backgrounds or a neutral text color on bright backgrounds.

### Setting a console color

The color tools allows you to set a console color either using the kernel color type, such as a neutral text color, or using a `Color` instance to select a custom color. The following functions are available:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static void SetConsoleColor(KernelColorType colorType)
public static void SetConsoleColor(KernelColorType colorType, bool Background)
public static void SetConsoleColor(Color ColorSequence, bool Background = false)
public static bool TrySetConsoleColor(KernelColorType colorType)
public static bool TrySetConsoleColor(KernelColorType colorType, bool Background)
public static bool TrySetConsoleColor(Color ColorSequence, bool Background)
```
{% endcode %}

In addition to setting the foreground color, you can also make it set the background color by passing `true` to `background` argument in all the supported console color setting functions above.

### Parsing colors

This allows you to easily parse either the color specifier string, the color number from 0 to 255, or the RGB color level values from 0 to 255. The following functions are available:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static bool TryParseColor(string ColorSpecifier)
public static bool TryParseColor(int ColorNum)
public static bool TryParseColor(int R, int G, int B)
```
{% endcode %}

The following functions are listed:

* The first function takes a color specifier and parses it.
* The second function takes a color number and parses it.
* The third function takes RGB color values and parses them.

### Getting a random color

You can get a random color of any type using any of the three functions:

{% code title="KernelColorTools.cs" lineNumbers="true" %}
```csharp
public static Color GetRandomColor(bool selectBlack = true)
public static Color GetRandomColor(ColorType type, bool selectBlack = true)
public static Color GetRandomColor(ColorType type, int minColor, int maxColor, int minColorR, int maxColorR, int minColorG, int maxColorG, int minColorB, int maxColorB)
```
{% endcode %}

Here's an explanation of what each version does:

* The first version only allows you to choose whether you need to select the black color or not. It returns a random color in its true color form.
* The second version allows you to choose a color type, along with the above black color selection. It returns a random color in the color type that you select.
* The third version allows you to choose a color type and several of the color ranges.
  * `minColor` to `maxColor`: Value can be from 0 to 16 if the type is 16 colors, or from 0 to 255 if the type is 256 colors. Ignored for true color randomization.
  * `minColorR` to `maxColorR`: Red level of the color range. Only applies to true color randomization.
  * `minColorG` to `maxColorG`: Green level of the color range. Only applies to true color randomization.
  * `minColorB` to `maxColorB`: Blue level of the color range. Only applies to true color randomization.

When you turn off black color selection, the function skips the color under the following conditions:

* If the color type is true color, it ignores any color that has all the RGB levels of below 30, such as `29;29;29`.
* If the color type is not true color, it ignores the following colors:
  * `ConsoleColors.Black`
  * `ConsoleColors.Grey0`
  * `ConsoleColors.Grey3`
  * `ConsoleColors.Grey7`
