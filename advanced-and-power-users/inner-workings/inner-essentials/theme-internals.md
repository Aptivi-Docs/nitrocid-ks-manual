---
description: Coloring things...
---

# 🎨 Theme Internals

Nitrocid KS first came with color theme support in the fourth major version, 0.0.4, but only supported 16 colors defined by the `ConsoleColor` enumeration. Since then, various themes have been added to the point that we once reached 95+ themes before going down to 65+ themes.

Themes for the kernel consist of color information for each kernel color type. They are made with a simple JSON syntax that's easy to use. Here's the format of each theme JSON file:

```json
{
    "Metadata": {
        "Name": "Theme name",
        "Description": "This is my theme",
        "IsEvent": false,
        "StartMonth": 2,
        "StartDay": 1,
        "EndMonth": 2,
        "EndDay": 22,
        "Calendar": "Gregorian",
        "Localizable": true
    },
    "InputColor": "15",
    "LicenseColor": "15",
    "ContKernelErrorColor": "15",
    (...)
}
```

We'll explain things one by one. The `Metadata` key consists of some basic information about the theme, like the name and the description. Themes can also be event-based by setting the appropriate property.

* `Name`: Display name of the theme
* `Description`: Short and concise description of the theme
* `IsEvent`: Indicates whether the theme is for a specific event (holidays, celebrations, etc.) **\[optional]**
* `StartMonth`: The month in which the event starts **\[optional]**
* `StartDay`: The day in which the event starts **\[optional]**
* `EndMonth`: The month in which the event ends **\[optional]**
* `EndDay`: The day in which the event ends **\[optional]**
* `Calendar`: The calendar to use, such as Hijri, Chinese, etc. **\[optional]**
* `Localizable`: Whether the description is localizable **\[internal, optional]**

What follows the metadata is a list of available kernel color types and their color representations using Terminaux's supported color formats, which are linked in the below page:

{% content-ref url="http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-sequences" %}
[Color Sequences](http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-sequences)
{% endcontent-ref %}

{% hint style="warning" %}
Make sure that the event start month and day is earlier than the end month and day. The theme parser will swap the day values and will add a year (end month is bigger than the start) if it detects that the start date is later than the end date (i.e. events can't end before they start).
{% endhint %}

### Using `ThemeInfo` to get theme information

To get theme information for a specific theme, you need to use the `ThemeInfo` constructor. The below constructors can be used:

* `ThemeInfo()`
  * This gives you a new instance of `ThemeInfo` with the default theme parameters
* `ThemeInfo(themePath)`
  * This gives you a new instance of `ThemeInfo` with the theme parameters from the given theme JSON file
* `ThemeInfo(ThemeFileStream)`
  * This gives you a new instance of `ThemeInfo` with the theme parameters from the given stream containing the theme JSON contents

{% hint style="warning" %}
`ThemeInfo()` constructor with theme names is now deprecated in favor of the theme packs. Please use the `GetInstalledThemes()` output and get the theme info instance from there instead.
{% endhint %}

### Checking to see if a theme exists

There is a function that lets you check to see if a built-in or an addon theme exists. `IsThemeFound()` is usable for such themes and can be provided a name of the theme.

### Color conversion

Your theme files can also support any specifier, as long as the specifier is supported by Terminaux. For a quick reminder, Terminaux supports the three true-color specifiers, alongside the color name or the color number, if you intend to use another color model to select colors:

* RGB: Red, Green, and Blue.
  * `<RRR>;<GGG>;<BBB>`
  * where the three variables can be from 0 to 255.
* CMYK: Cyan, Magenta, and Yellow with the Black Key.
  * `cmyk:<CCC>;<MMM>;<YYY>;<KKK>`
  * where these variables can be from 0 to 100.
* HSL: Hue, Saturation, and Luminance (or Lightness).
  * `hsl:<HHH>;<SSS>;<LLL>`
  * where the Hue can be from 0 to 360 _**degrees**_ and _**not radians**_.
  * where the Saturation and the Luminance can be from 0 to 100.

The commands provided by the color conversion Extras addon help you convert from a color model, such as RGB, to another color model, such as CMYK.

`KernelColorConversionTools` provides you all possible conversion methods to convert a color model to another color model to generate appropriate color specifiers converted to the target unit to create new `Color` instances for your mod's appearance.

For example, if you have Cyan, Magenta, and Yellow values and you want a hex code of it, you can use one of the following function overloads of `ConvertFromCmykToHex()`:

* `ConvertFromCmykToHex(int C, int M, int Y, int K)`
* `ConvertFromCmykToHex(string CMYKSequence)`

### Color wheel

The new color wheel documentation is coming soon, so stay tuned for updates on the Terminaux documentation:

{% content-ref url="http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-wheel" %}
[Color Wheel](http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-wheel)
{% endcontent-ref %}
