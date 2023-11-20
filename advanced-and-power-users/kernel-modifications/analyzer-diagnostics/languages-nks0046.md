---
description: Use CultureManager.UpdateCulture
---

# 📉 Languages - NKS0046

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>CultureInfo.CurrentUICulture</code> instead of <code>CultureManager.UpdateCulture()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>CultureManager.UpdateCulture()</code> instead of setting <code>CultureInfo.CurrentUICulture</code></td></tr><tr><td>Description</td><td><code>CultureManager.UpdateCulture()</code> sets a current culture without affecting the host system. It also updates the settings so that it holds the new culture.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `CurrentUICulture` from the `CultureInfo` class found in the `System.Globalizaiton` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    CultureInfo.CurrentUICulture = CultureInfo.GetCultureInfo("en-US");
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    CultureManager.UpdateCulture("en-US");
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.
