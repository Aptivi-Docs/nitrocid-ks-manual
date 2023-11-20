---
description: Use KernelPlatform.IsOnWindows()
---

# 📉 Kernel - NKS0037

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Environment.OSVersion.Platform == PlatformID.Win32NT</code> instead of <code>KernelPlatform.IsOnWindows()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.IsOnWindows()</code> instead of <code>Environment.OSVersion.Platform == PlatformID.Win32NT</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.IsOnWindows()</code> is more readable and less verbose than <code>Environment.OSVersion.Platform == PlatformID.Win32NT</code>.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the comparison of `Environment.OSVersion.Platform` against the `Win32NT` value.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = Environment.OSVersion.Platform == PlatformID.Win32NT;
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = KernelPlatform.IsOnWindows();
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
