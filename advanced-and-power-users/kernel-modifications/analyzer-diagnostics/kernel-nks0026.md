---
description: Use TimeDateRenderers.RenderDate()
---

# 📉 Kernel - NKS0026

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>TimeDateTools.KernelDateTime.ToString</code> instead of <code>TimeDateRenderers.RenderDate()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TimeDateRenderers.RenderDate()</code> instead of <code>TimeDateTools.KernelDateTime.ToString</code></td></tr><tr><td>Description</td><td><code>TimeDateRenderers.RenderDate()</code> respects your kernel settings when rendering date.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `KernelDateTime.ToString` from the `TimeDateTools` class found in the `KS.Kernel.Time` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = TimeDateTools.KernelDateTime.ToString();
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    string value = TimeDateRenderers.RenderDate();
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
