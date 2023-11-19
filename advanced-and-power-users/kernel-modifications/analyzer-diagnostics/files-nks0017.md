---
description: Use Removing.RemoveDirectory()
---

# 📉 Files - NKS0017

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Directory.Delete</code> instead of <code>Removing.RemoveDirectory()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>Removing.RemoveDirectory()</code> instead of <code>Directory.Delete</code></td></tr><tr><td>Description</td><td><code>Removing.RemoveDirectory()</code> neutralizes the provided path to its absolute correct path, while <code>Directory.Delete</code> operates at the executable directory (<code>Environment.CurrentDirectory</code>), which may not be what you want.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `Delete` from the standard `Directory` class found in the `System.IO` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Directory.Delete("test");
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Removing.RemoveDirectory("test");
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
