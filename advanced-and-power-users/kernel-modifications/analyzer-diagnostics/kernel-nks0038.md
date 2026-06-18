---
description: Use KernelPlatform.IsOnUnix()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/kernel-nks0038
---

# Kernel - NKS0038

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Environment.OSVersion.Platform == PlatformID.Unix</code> instead of <code>KernelPlatform.IsOnUnix()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.IsOnUnix()</code> instead of <code>Environment.OSVersion.Platform == PlatformID.Unix</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.IsOnUnix()</code> is more readable and less verbose than <code>Environment.OSVersion.Platform == PlatformID.Unix</code>.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the comparison of `Environment.OSVersion.Platform` against the `Unix` value.

`Environment.OSVersion.Platform` is an ancient way of determining the current operating system that Nitrocid is running on. As a result, it doesn't implement the macOS operating system detection, since it was considered as Unix.

As a result, `KernelPlatform` implements a handful of platform detection functions to allow you to more accurately detect your platform. Also, it simplifies the complicated platform checking statements to its simpler equivalent.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = Environment.OSVersion.Platform == PlatformID.Unix;
</strong>}
</code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    bool value = KernelPlatform.IsOnUnix();
</strong>}
</code></pre>
