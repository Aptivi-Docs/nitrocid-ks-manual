---
description: Use KernelPlatform.IsOnUnix()
---

# 📉 Kernel - NKS0040

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>RuntimeInformation.IsOSPlatform(OSPlatform.Linux)</code> instead of <code>KernelPlatform.IsOnUnix()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.IsOnUnix()</code> instead of <code>RuntimeInformation.IsOSPlatform(OSPlatform.Linux)</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.IsOnUnix()</code> is more readable and less verbose than <code>RuntimeInformation.IsOSPlatform(OSPlatform.Linux)</code>.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `IsOSPlatform` from the `RuntimeInformation` class found in the `System.Runtime.InteropServices` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = RuntimeInformation.IsOSPlatform(OSPlatform.Linux);
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = KernelPlatform.IsOnUnix();
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.