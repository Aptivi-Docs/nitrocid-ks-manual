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
        "Localizable": true
    },
    "InputColor": "15",
    "LicenseColor": "15",
    "ContKernelErrorColor": "15",
    (...)
}
```

{% hint style="info" %}
`ThemeInfo()` constructor with theme names is now deprecated in favor of the theme packs. Please use the `GetInstalledThemes()` output and get the theme info instance from there instead.
{% endhint %}

We'll explain things one by one. The `Metadata` key consists of some basic information about the theme, like the name and the description. Themes can also be event-based by setting the appropriate property.

* `Name`: Display name of the theme
* `Description`: Short and concise description of the theme
* `IsEvent`: Indicates whether the theme is for a specific event (holidays, celebrations, etc.)
* `StartMonth`: The month in which the event starts
* `StartDay`: The day in which the event starts
* `EndMonth`: The month in which the event ends
* `EndDay`: The day in which the event ends
* `Localizable`: Whether the description is localizable (internal)

What follows the metadata is a list of available kernel color types and their color representations using Terminaux's supported color formats, which are linked in the below page:

{% content-ref url="http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-sequences" %}
[Color Sequences](http://127.0.0.1:5000/s/G0KrE9Uk2AiblqjWtpAo/usage/how-to-use/color-sequences)
{% endcontent-ref %}

{% hint style="danger" %}
Due to limitations in the theme parser, it's crucial that you provide color values for all the kernel color types without any exception. Otherwise, it'll throw errors.
{% endhint %}

{% hint style="warning" %}
Make sure that the event start month and day is earlier than the end month and day. The theme parser will swap these values if it detects that the start date is later than the end date (i.e. events can't end before they start).
{% endhint %}
