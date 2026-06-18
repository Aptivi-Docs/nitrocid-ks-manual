---
description: Use TimeZones.GetCurrentZoneInfo()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/kernel-nks0024
---

# Kernel - NKS0024

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>TimeZoneInfo.Local</code> instead of <code>TimeZones.GetCurrentZoneInfo()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TimeZones.GetCurrentZoneInfo()</code> instead of <code>TimeZoneInfo.Local</code></td></tr><tr><td>Description</td><td><code>TimeZones.GetCurrentZoneInfo()</code> gets your local time zone and respects your kernel settings based on that. It either gets your local time zone from your system or from your kernel configuration.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of `Local` from the standard `TimeZoneInfo` class found in the `System` namespace.

`TimeZoneInfo.Local` gives you a `TimeZoneInfo` instance containing information about your computer's current timezone. However, the kernel has been given a brand new feature that allows you to choose your custom timezone without affecting the host system.

As a result, you should use `TimeZones.GetCurrentZoneInfo()` as it respects your kernel settings regarding the timezone.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var zone = TimeZoneInfo.Local;
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var zone = TimeZones.GetCurrentZoneInfo();
</strong>}
</code></pre>
