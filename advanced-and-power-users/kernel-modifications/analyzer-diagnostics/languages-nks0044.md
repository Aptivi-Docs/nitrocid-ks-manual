---
description: Use CultureManager.CurrentCult
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/languages-nks0044
---

# Languages - NKS0044

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>CultureInfo.CurrentUICulture</code> instead of <code>CultureManager.CurrentCulture</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>CultureManager.CurrentCulture</code> instead of <code>CultureInfo.CurrentUICulture</code></td></tr><tr><td>Description</td><td><code>CultureManager.CurrentCulture</code> gives you a current culture that is set by the kernel settings without affecting the host system.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `CurrentUICulture` from the `CultureInfo` class found in the `System.Globalization` namespace.

The `CultureInfo.CurrentUICulture` property gives you your current UI culture for your applications. However, Nitrocid is not a GUI application, so we've decided to make our own culture handler that respects your kernel settings.

It's advisable to use the `CultureManager.CurrentCulture` property so that your mod can respect the kernel settings when it comes to cultures.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var culture = CultureInfo.CurrentUICulture;
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var culture = CultureManager.CurrentCulture;
</strong>}
</code></pre>
