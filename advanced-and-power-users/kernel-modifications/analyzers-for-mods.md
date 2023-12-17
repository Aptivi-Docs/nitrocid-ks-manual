---
description: What are analyzers?
---

# 📉 Analyzers for Mods

Analyzers, in .NET, are tools that allow you to check the quality of your code and to fix common design pitfalls in your code. These fixes typically tailor the use of better features or the removal of unnecessary code.

Similarly, we provide you with analyzers that detect the usage of non-Nitrocid methods and classes and provide you fixes that make use of Nitrocid methods and classes as good alternatives. These analyzers are applicable only to Nitrocid mods.

We provide you two types of analyzers for your Nitrocid mods:

* Visual Studio-based analyzers that allow you to analyze your mods while you're working on them in Visual Studio.
* Standalone analyzers that allow you to analyze your mod code outside Visual Studio.

In this page, we'll give you instructions on how to install such analyzers. Choose the analyzer type based on your preferences. Meanwhile, you can consult the analyzer diagnostics page linked below:

{% content-ref url="analyzer-diagnostics/" %}
[analyzer-diagnostics](analyzer-diagnostics/)
{% endcontent-ref %}

## Installation

There are two types of Nitrocid analyzers as highlighted above. This section shows you how to analyze your code with either Visual Studio and the standalone analyzer. The mod analyzer package found in the release contains both the standalone analyzer and the Visual Studio-based analyzer.

### Visual Studio

In order to install the Visual Studio-based analyzer for Nitrocid mods, follow the below steps:

1. Extract the `mod-analyzer` package using your archive manager.
2.  Go to the directory of the analyzer that you've extracted, and scroll down until you see `Nitrocid.Analyzers.Vsix.vsix`

    <figure><img src="../../.gitbook/assets/image_2023-12-17_114150379.png" alt=""><figcaption></figcaption></figure>
3. Follow the instructions on the installer until it completes the installation
4. Open your mod project on Visual Studio
5. Start working on your mod, and you'll see `NKS` analyzers.

### Standalone Analyzer

In case you can't use Visual Studio-based analyzer for your mods, you can use the standalone analyzer. To use it, follow the steps:

1. Open the command prompt
2. Go to the directory where the standalone analyzer is located. Use `cd` to change the directory.
3.  Run `dotnet Nitrocid.StandaloneAnalyzer.dll path/to/mod.sln`\


    <figure><img src="../../.gitbook/assets/image_2023-12-17_115217784.png" alt=""><figcaption></figcaption></figure>
