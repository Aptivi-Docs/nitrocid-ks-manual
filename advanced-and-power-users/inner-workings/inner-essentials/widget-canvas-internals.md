---
description: Canvas internals are here.
icon: presentation-screen
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/widget-canvas-internals
---

# Widget Canvas Internals

<figure><img src="../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Widget Canvas provides an API that allows you to programmatically manage and render the widget canvases. All widget canvas tools are found in the `Nitrocid.Base.Misc.Widgets.Canvas` namespace, which is part of the broader Widgets namespace that contains all widget-related classes.

***

## <mark style="color:$primary;">Widget canvas functions</mark>

This API provides a list of functions that allow you to manage the widget canvases, such as getting render info instances and rendering the widgets through the obtained info.

Available functions include:

* Obtaining a list of widget render info instances from either a file (`GetRenderInfosFromFile`) or a JSON representation (`GetRenderInfos`)
* Exporting render information instances to a JSON representation (`ExportRenderInfos`) and saving them to a file (`SaveRenderInfos`)
* Rendering the widgets from the list of such instances (`RenderFromInfos`)

***

## <mark style="color:$primary;">Widget render information class</mark>

An instance of a widget render information class is public, and can be accessed (but not modified) by any mod.

<details>

<summary>Properties of the info class</summary>

You can use the following properties:

<table><thead><tr><th width="140.3333740234375">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>WidgetName</code></td><td>Specifies a widget by name to render</td></tr><tr><td><code>Bordered</code></td><td>Renders the border around the widget</td></tr><tr><td><code>Relative</code></td><td>Use relative sizes (by margins)</td></tr><tr><td><code>Coordinates</code></td><td>Left and top positions of the widget</td></tr><tr><td><code>Size</code></td><td>Width and height of the widget</td></tr><tr><td><code>Margin</code></td><td>Margin size of the widget</td></tr></tbody></table>

</details>

<details>

<summary>JSON structure</summary>

Any mod can render a widget canvas, with the JSON information that satisfies the following format:

{% code expandable="true" %}
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
{% endcode %}

The only required options are `widgetName`, which chooses a widget to render, `left`, for the left position that is zero-based, and `top`, for the top position that is zero-based.

#### <mark style="color:$primary;">Optional properties</mark>

The rest of the properties are defined as follows:

<table><thead><tr><th width="120.333251953125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>bordered</code></td><td>Whether to draw a border around the widget or not.</td></tr><tr><td><code>relative</code></td><td>Whether to use relative widths and heights or not.</td></tr><tr><td><code>options</code></td><td>Specifies the options for the widgets.</td></tr></tbody></table>

#### <mark style="color:$primary;">Relative widths and heights</mark>

If the relative widths and heights are turned on, the following options apply:

<table><thead><tr><th width="180.333251953125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>widthLeftMargin</code></td><td>Left margin for the width of the console window.</td></tr><tr><td><code>widthRightMargin</code></td><td>Right margin for the width of the console window.</td></tr><tr><td><code>heightTopMargin</code></td><td>Top margin for the height of the console window.</td></tr><tr><td><code>heightBottomMargin</code></td><td>Bottom margin for the height of the console window.</td></tr></tbody></table>

Else, the following options apply:

<table><thead><tr><th width="180.333251953125">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>width</code></td><td>Width of the widget.</td></tr><tr><td><code>height</code></td><td>Height of the widget.</td></tr></tbody></table>

#### <mark style="color:$primary;">Widget-specific options</mark>

Some widgets, especially those that support customization options, provide their own options. The following options are available:

<table><thead><tr><th width="175.33331298828125">Widget</th><th width="109.6666259765625">Option</th><th>Description</th></tr></thead><tbody><tr><td><code>TextWidget</code></td><td><code>text</code></td><td>Specifies the text to display.</td></tr><tr><td><code>Photo</code></td><td><code>photoPath</code></td><td>Specifies a path to the image to be displayed.</td></tr><tr><td><code>NotificationIcons</code></td><td><code>alignment</code></td><td>Text alignment for the notification icons.</td></tr></tbody></table>

</details>
