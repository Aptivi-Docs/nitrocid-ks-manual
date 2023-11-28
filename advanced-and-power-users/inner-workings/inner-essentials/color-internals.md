---
description: All of the colors!
---

# ⛱ Color Internals

Nitrocid KS uses Terminaux to manipulate with the colors and configure them for the kernel to use. The kernel employs several of the color types for the kernel components, your addons, or your mods to use when writing text using the Nitrocid's console writer.

**TODO: Fill in the blanks for this section. We'll go back to it later.**

## Color tools

Nitrocid KS provides you a built-in color tools that allows you to manipulate with the colors in various ways. The following types of manipulation are available:

**TODO: More tools TBD.**

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
