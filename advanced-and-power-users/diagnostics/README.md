---
description: Trying to find a defect in the kernel? Great! Thanks for your contribution!
---

# 🦠 Diagnostics

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

The simulated kernel contains its own diagnostic tools to allow you to diagnose what's wrong with a feature. These diagnostic tools help you analyze the kernel for what it's doing and for how it failed.

There are two ways to diagnose the kernel: in-kernel debugging, and using Visual Studio.

## In-kernel Debugging

In-kernel debugging allows you to use its own built-in tools to debug the kernel and its components. For more information, head to the below page.

{% content-ref url="debugging/" %}
[debugging](debugging/)
{% endcontent-ref %}

## Visual Studio

This way of debugging is only available if you have Visual Studio installed. If you have the source code of the kernel cloned from our GitHub, you can attach the Nitrocid KS process to the debugger. Here's how, assuming that Nitrocid KS is already open:

1. Open Visual Studio to the empty project
2. Right-click on `Debug` -> `Attach to Process`
3. Find `Nitrocid.exe`
4. Click on `Attach`
5. In case Visual Studio is asking for source files, point to a file within the Nitrocid KS source
