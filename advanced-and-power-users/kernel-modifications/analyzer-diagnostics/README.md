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

<table><thead><tr><th width="132">Diag. ID</th><th width="106">Section</th><th data-type="content-ref">Page</th></tr></thead><tbody><tr><td><code>NKS0001</code></td><td>Text</td><td><a href="text-nks0001.md">text-nks0001.md</a></td></tr></tbody></table>
{% endtab %}

{% tab title="Suggestions" %}
Currently, there are no analyzers which generate suggestions yet. However, we'll plan to add more analyzers.
{% endtab %}
{% endtabs %}

{% hint style="info" %}
It's vital to follow the analyzer recommendations to get the best mod code according to the standards.
{% endhint %}
