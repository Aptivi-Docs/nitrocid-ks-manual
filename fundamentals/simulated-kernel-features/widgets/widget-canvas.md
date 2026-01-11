---
description: What are widget canvases, anyway?
icon: presentation-screen
---

# Widget Canvas

<figure><img src="../../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Widget Canvas API allows you to extend both the login and the homepage by using pages of widgets to allow you to store more information, including the date and the time, the RSS feeds, images, and so on. It uses a set of JSON files that describe a single page under the following folders inside the Nitrocid KS configuration directory:

* `LogonPages`: A directory that stores widget pages for the modern logon screen
* `HomepagePages`: A directory that stores widget pages for The Nitrocid Homepage

You can create a JSON file by creating it under one of the above directories, depending on the context, and make an array of widget rendering information. You can consult the below page for more information.

{% content-ref url="../../../advanced-and-power-users/inner-workings/inner-essentials/widget-canvas-internals.md" %}
[widget-canvas-internals.md](../../../advanced-and-power-users/inner-workings/inner-essentials/widget-canvas-internals.md)
{% endcontent-ref %}

{% hint style="warning" %}
Widget canvases are only supported in the modern logon handler and in The Nitrocid Homepage. Any custom logon handlers are currently not supported with Widget Canvas API.
{% endhint %}

In the modern logon screen and in the homepage, you can switch between pages by pressing the left and the right arrow keys. Pages are processed sequentially and in the alphanumerical order, in the same way as how the files are sorted.

{% hint style="warning" %}
If you have to show the widget canvases in a specific order, you'll have to rename their files to start with the numbers. Beware that you'll have to pad zeroes to avoid issues regarding filesystem sorting, such as `01-page.json`, `02-page.json`, and so on.
{% endhint %}
