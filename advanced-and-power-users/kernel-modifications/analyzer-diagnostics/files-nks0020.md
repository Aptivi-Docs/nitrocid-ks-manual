---
description: Use Checking.Exists()
---

# 📉 Files - NKS0020

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Path.Exists</code> instead of <code>Checking.Exists()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>Checking.Exists()</code> instead of <code>Path.Exists</code></td></tr><tr><td>Description</td><td><code>Checking.Exists()</code> neutralizes the provided path to its absolute correct path, while <code>Path.Exists</code> operates at the executable Path (<code>Environment.CurrentPath</code>), which may not be what you want.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `Exists` from the standard `Path` class found in the `System.IO` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Path.Exists("test.txt");
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    Checking.Exists("test.txt");
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
