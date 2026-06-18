---
description: Trying to find a defect in the kernel? Great! Thanks for your contribution!
icon: virus-covid
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/diagnostics
---

# Diagnostics

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

The simulated kernel contains its own diagnostic tools to allow you to diagnose what's wrong with a feature. These diagnostic tools help you analyze the kernel for what it's doing and for how it failed.

There are two ways to diagnose the kernel: in-kernel debugging, and using Visual Studio.

***

## <mark style="color:$primary;">In-kernel Debugging</mark>

In-kernel debugging allows you to use its own built-in tools to debug the kernel and its components. For more information, head to the below page.

{% content-ref url="debugging/" %}
[debugging](debugging/)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Visual Studio</mark>

This way of debugging is only available if you have Visual Studio installed. If you have the source code of the kernel cloned from our GitHub, you can attach the Nitrocid KS process to the debugger.

Here's how, assuming that Nitrocid KS is already open:

{% stepper %}
{% step %}
#### <mark style="color:$primary;">Open Visual Studio</mark>

Open Visual Studio to the empty project
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Attach to process</mark>

Right-click on `Debug` -> `Attach to Process`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Find Nitrocid</mark>

Find `Nitrocid.exe`
{% endstep %}

{% step %}
#### <mark style="color:$primary;">Attach it</mark>

Click on `Attach`
{% endstep %}
{% endstepper %}

{% hint style="info" %}
In case Visual Studio is asking for source files, point to a file within the Nitrocid KS source
{% endhint %}

### <mark style="color:$primary;">`KernelException`</mark> <mark style="color:$primary;">Class</mark>

`KernelException` is an exception class that uses the exception type to give you a possible cause for each exception type. The kernel (and your mods) make extensive use of this exception to signal an error, but this class can also hold an inner exception of either the nested `KernelException` class or any of the `Exception` classes.

Each `KernelException` instance holds the following properties:

<table><thead><tr><th width="240.00006103515625">Property</th><th>Description</th></tr></thead><tbody><tr><td><code>ExceptionType</code></td><td>Specifies the exception type using the <code>KernelExceptionType</code> enumeration.</td></tr><tr><td><code>OriginalExceptionMessage</code></td><td>Specifies the original exception message before being processed.</td></tr><tr><td><code>KernelExceptionMessage</code></td><td>Shows a full message from the exception type.</td></tr></tbody></table>
