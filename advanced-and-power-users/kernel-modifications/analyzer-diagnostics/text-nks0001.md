---
description: Use TextTools.FormatString() instead of string.Format()
icon: chart-mixed
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/analyzer-diagnostics/text-nks0001
---

# Text - NKS0001

This analyzer provides the following strings:

<table><thead><tr><th width="174">Context</th><th>String</th></tr></thead><tbody><tr><td>Error List</td><td>Caller uses <code>string.Format()</code> instead of <code>TextTools.FormatString()</code></td></tr><tr><td>Suggestion Box</td><td>Use <code>TextTools.FormatString()</code> instead of <code>string.Format()</code></td></tr><tr><td>Description</td><td><code>TextTools.FormatString()</code> uses the error handler to handle unknown formatting errors and returns the unformatted string if such errors happen, but <code>string.Format()</code> immediately throws.</td></tr></tbody></table>

***

## <mark style="color:$primary;">Extended Description</mark>

This code analyzer detects the usage of the standard `string.Format()` method from the regular .NET core libraries, and highlights the relevant parts as yellow squiggly lines indicating a warning.

The reason is that `string.Format()` tries to format any text within the .NET string formatting syntax defined in [this link](https://learn.microsoft.com/en-us/dotnet/api/system.string.format), and throws an exception if any of these syntaxes are invalid. However, `TextTools.FormatString()` is clever at handling such exceptions and returns the unformatted string in case formatting fails.

Also, `TextTools.FormatString()` doesn't attempt to format any string and returns the plain string that's passed to it if there are no arguments to be passed to the formatter, making it impossible to crash if it was used without arguments accidentally or intentionally.

This analyzer detects the usage of `string.Format()` and fixes it by replacing the call with `TextTools.FormatString()`, importing the `Textify.General` namespace if necessary.

***

## <mark style="color:$primary;">Analysis Comparison</mark>

To get a brief insight about how this analyzer works, compare the two code blocks shown to you below:

### <mark style="color:$primary;">Before the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    TextWriterColor.Write(string.Format("Hello, {0}!", "Nitrocid"));
</strong></code></pre>

### <mark style="color:$primary;">After the fix</mark>

<pre class="language-csharp" data-title="Somewhere in your mod code..." data-line-numbers><code class="lang-csharp">public static void MyFunction() =>
<strong>    TextWriterColor.Write(TextTools.FormatString("Hello, {0}!", "Nitrocid"));
</strong></code></pre>
