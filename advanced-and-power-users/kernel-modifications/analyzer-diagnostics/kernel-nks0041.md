---
description: Use KernelPlatform.IsOnMacOs()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/kernel-nks0041
---

# Kernel - NKS0041

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>RuntimeInformation.IsOSPlatform(OSPlatform.OSX)</code> instead of <code>KernelPlatform.IsOnMacOS()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.IsOnMacOS()</code> instead of <code>RuntimeInformation.IsOSPlatform(OSPlatform.OSX)</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.IsOnMacOS()</code> is more readable and less verbose than <code>RuntimeInformation.IsOSPlatform(OSPlatform.OSX)</code>.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `IsOSPlatform` from the `RuntimeInformation` class found in the `System.Runtime.InteropServices` namespace.

`RuntimeInformation.IsOSPlatform` is a modern way of determining the current operating system that Nitrocid is running on. However, this isn't live detection.

As a result, `KernelPlatform` implements a handful of platform detection functions to allow you to more accurately detect your platform. Also, it simplifies the complicated platform checking statements to its simpler equivalent.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = RuntimeInformation.IsOSPlatform(OSPlatform.OSX);
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = KernelPlatform.IsOnMacOS();
</strong>}
</code></pre>
