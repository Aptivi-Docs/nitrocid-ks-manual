---
description: Here's a list of analyzer diagnostics.
---

# 📈 Analyzer Diagnostics

Nitrocid KS provides you with its own code analyzer to check your mod code for anything odd, such as the usage of a function that already exists in Nitrocid's code or possible code refactorings to suit the selected mod API version.

This code analyzer runs under both the CLI and the Visual Studio GUI (as a .VSIX extension). It provides suggestions as to how to improve your mod code.

The following code analyzers are shipped, with links to each page:

{% tabs %}
{% tab title="Errors" %}
Currently, there are no analyzers which generate errors yet. However, we'll plan to add more analyzers.
{% endtab %}

{% tab title="Warnings" %}
The following analyzers generate warnings:

<table><thead><tr><th width="139">Diag. ID</th><th data-type="content-ref">Page</th></tr></thead><tbody><tr><td><code>NKS0001</code></td><td><a href="text-nks0001.md">text-nks0001.md</a></td></tr><tr><td><code>NKS0002</code></td><td><a href="consolebase-nks0002.md">consolebase-nks0002.md</a></td></tr><tr><td><code>NKS0003</code></td><td><a href="consolebase-nks0003.md">consolebase-nks0003.md</a></td></tr></tbody></table>
{% endtab %}

{% tab title="Suggestions" %}
The following analyzers generate suggestions that are shown under the Messages section of the Errors List on your Visual Studio:

<table><thead><tr><th width="140">Diag. ID</th><th data-type="content-ref">Page</th></tr></thead><tbody><tr><td><code>NKS0004</code></td><td><a href="consolebase-nks0004.md">consolebase-nks0004.md</a></td></tr><tr><td><code>NKS0005</code></td><td><a href="consolebase-nks0005.md">consolebase-nks0005.md</a></td></tr><tr><td><code>NKS0006</code></td><td><a href="consolebase-nks0006.md">consolebase-nks0006.md</a></td></tr><tr><td><code>NKS0007</code></td><td><a href="consolebase-nks0007.md">consolebase-nks0007.md</a></td></tr><tr><td><code>NKS0008</code></td><td><a href="consolebase-nks0008.md">consolebase-nks0008.md</a></td></tr></tbody></table>
{% endtab %}
{% endtabs %}

{% hint style="info" %}
It's vital to follow the analyzer recommendations to get the best mod code according to the standards.
{% endhint %}
