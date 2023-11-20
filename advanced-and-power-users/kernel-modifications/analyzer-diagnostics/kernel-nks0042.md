---
description: Use KernelPlatform.GetTerminalEmulator()
---

# 📉 Kernel - NKS0042

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code> instead of <code>KernelPlatform.GetTerminalEmulator()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>KernelPlatform.GetTerminalEmulator()</code> instead of <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code></td></tr><tr><td>Description</td><td><code>KernelPlatform.GetTerminalEmulator()</code> is more readable and less verbose than <code>Environment.GetEnvironmentVariable("TERM_PROGRAM")</code>.</td></tr></tbody></table>

### Extended Description

This code analyzer detects the usage of `GetEnvironmentVariable("TERM_PROGRAM")` from the `Environment` class found in the `System` namespace.

**TODO: Populate this section once we finish adding analyzers tracked internally.**

### Analysis Comparison

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

#### Before the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var value = Environment.GetEnvironmentVariable("TERM_PROGRAM");
</strong>}
</code></pre>

#### After the fix

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction()
{
<strong>    var value = KernelPlatform.GetTerminalEmulator();
</strong>}
</code></pre>

### Suppression

You can suppress this suggestion by including it in the appropriate place, whichever is convenient.

For more information about how to suppress any warning issued by the Nitrocid analyzer, visit the below page:

{% embed url="https://learn.microsoft.com/en-us/dotnet/fundamentals/code-analysis/suppress-warnings" %}

### Recommendation

We recommend that every caller which use this function use the recommended abovementioned method.