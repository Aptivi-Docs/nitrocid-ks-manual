---
description: Use TimeDateRenderersUtc.RenderTimeUtc()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/kernel-nks0031
---

# Kernel - NKS0031

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>TimeDateTools.KernelDateTimeUtc.ToString</code> instead of <code>TimeDateRenderersUtc.RenderTimeUtc()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TimeDateRenderersUtc.RenderTimeUtc()</code> instead of <code>TimeDateTools.KernelDateTimeUtc.ToString</code></td></tr><tr><td>Description</td><td><code>TimeDateRenderersUtc.RenderTime</code>Utc<code>()</code> respects your kernel settings when rendering time.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `KernelDateTimeUtc.ToString` from the `TimeDateTools` class found in the `KS.Kernel.Time` namespace.

`TimeDateTools.KernelDateTime` contains an override to a function that converts that instance of the current date and time to its string representation. However, there is a function dedicated to that, called `Render()` and its siblings, that renders your target time to its equivalent string representation and also respects your kernel settings.

Similarly, `TimeDateTools.KernelDateTimeUtc` has been given the same treatment, because you can also use the `RenderUtc()` function and its siblings.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = TimeDateTools.KernelDateTimeUtc.ToString();
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = TimeDateRenderersUtc.RenderTimeUtc();
</strong>}
</code></pre>
