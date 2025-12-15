---
description: Canvas internals are here.
icon: presentation-screen
---

# Widget Canvas Internals

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Widget Canvas provides an API that allows you to programmatically manage and render the widget canvases. All widget canvas tools are found in the `Nitrocid.Base.Misc.Widgets.Canvas` namespace, which is part of the broader Widgets namespace that contains all widget-related classes. This API provides a list of functions that allow you to manage the widget canvases, such as getting render info instances and rendering the widgets through the obtained info.

Available functions include:

* Obtaining a list of widget render info instances from either a file (`GetRenderInfosFromFile`) or a JSON representation (`GetRenderInfos`)
* Exporting render information instances to a JSON representation (`ExportRenderInfos`) and saving them to a file (`SaveRenderInfos`)
* Rendering the widgets from the list of such instances (`RenderFromInfos`)

An instance of a widget render information class is public, and can be accessed (but not modified) by any mod. You can use the following properties:

* `WidgetName`: Specifies a widget by name to render
* `Bordered`: Renders the border around the widget
* `Relative`: Use relative sizes (by margins)
* `Coordinates`: Left and top positions of the widget
* `Size`: Width and height of the widget
* `Margin`: Margin size of the widget

Any mod can render a widget canvas, with the JSON information that satisfies the following format:

```json
[
    {
        "widgetName": "DigitalClock",
        "bordered": true,
        "relative": true,
        "left": 3,
        "top": 1,
        "widthLeftMargin": 3,
        "widthRightMargin": 3,
        "heightTopMargin": 2,
        "heightBottomMargin": 1,
    },
    {
        "widgetName": "TextWidget",
        "left": 3,
        "top": 1,
        "options": {
            "text": "✅"
        }
    }
]
```

The only required options are `widgetName`, which chooses a widget to render, `left`, for the left position that is zero-based, and `top`, for the top position that is zero-based. The rest of the properties are defined as follows:

* `bordered`: Whether to draw a border around the widget or not
* `relative`: Whether to use relative widths and heights or not
  * If this option is on, the following options apply:
    * `widthLeftMargin`: Left margin for the width of the console window
    * `widthRightMargin`: Right margin for the width of the console window
    * `heightTopMargin`: Top margin for the height of the console window
    * `heightBottomMargin`: Bottom margin for the height of the console window
  * If this option is off, the following options apply:
    * `width`: Width of the widget
    * `height`: Height of the widget
* `options`: Specifies the options for the widgets, where the following apply:
  * `TextWidget`
    * `text`: Specifies the text to display
  * `Photo`
    * `photoPath`: Specifies a path to the image to be displayed
  * `NotificationIcons`
    * `alignment`: Text alignment for the notification icons
  * All widgets that support customization options.
