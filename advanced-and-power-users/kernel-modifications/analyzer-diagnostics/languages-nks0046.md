---
description: Use CultureManager.UpdateCulture
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/languages-nks0046
---

# Languages - NKS0046

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>CultureInfo.CurrentUICulture</code> instead of <code>CultureManager.UpdateCulture()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>CultureManager.UpdateCulture()</code> instead of setting <code>CultureInfo.CurrentUICulture</code></td></tr><tr><td>Description</td><td><code>CultureManager.UpdateCulture()</code> sets a current culture without affecting the host system. It also updates the settings so that it holds the new culture.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `CurrentUICulture` from the `CultureInfo` class found in the `System.Globalization` namespace.

The `CultureInfo.CurrentUICulture` property gives you your current UI culture for your applications. However, Nitrocid is not a GUI application, so we've decided to make our own culture handler that respects your kernel settings.

It's advisable to use the `CultureManager.UpdateCulture()` function so that your mod can load a new culture and save the kernel settings to make this change permanent across reboots.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    CultureInfo.CurrentUICulture = CultureInfo.GetCultureInfo("en-US");
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    CultureManager.UpdateCulture("en-US");
</strong>}
</code></pre>
