---
description: Please wait while we're processing your request...
icon: hourglass-end
---

# Progress Handlers

The progress handlers allow you to handle how you want to notify that there is progress going on. For long operations that are split to short operations, such as showing what files are being copied for every single file, you can use this facility to register and unregister your progress handlers.

When registration is complete, you should be notified about the progress of an operation, depending on how you defined the progress handling action.

Every progress handler can be created using the following constructor:

{% code title="ProgressHandler.cs" lineNumbers="true" %}
```csharp
public ProgressHandler(Action<double, string> progressAction, string context)
```
{% endcode %}

The progress handler manager allows you to register and unregister your progress handler, given that you already keep the progress handler handy in any way possible in case you want to unregister it.

{% code title="ProgressManager.cs" lineNumbers="true" %}
```csharp
public static void RegisterProgressHandler(ProgressHandler handler)
public static void UnregisterProgressHandler(ProgressHandler handler)
```
{% endcode %}

For example, this is the bit of code needed to register your progress handler.

{% code title="Example code" lineNumbers="true" %}
```csharp
var handler = new ProgressHandler((num, text) =>
    TextWriterColor.WriteKernelColor($"{num}% {text}", KernelColorType.Progress)
    , "General");
ProgressManager.RegisterProgressHandler(handler);
```
{% endcode %}

This is the bit of code to unregister your handler, given that you've kept the handler handy:

{% code title="Example code" lineNumbers="true" %}
```csharp
ProgressManager.UnregisterProgressHandler(handler);
```
{% endcode %}

After you register the handler, you can report the progress using the same context using one of the following functions:

```csharp
public static void ReportProgress(double progress, string context)
public static void ReportProgress(double progress, string context, string message)
public static void ReportProgress(double progress, string context, string message, params object[] vars)
```

Any call to one of these `ReportProgress()` functions with the correct context that is handled will follow it the progress indicator showing on your screen, or any other progress action, depending on how you're handling the progress.

For example, this is the simplest method to report the progress, assuming that this is reported inside a long operation loop:

{% code title="Example code" lineNumbers="true" %}
```csharp
ProgressManager.ReportProgress(progress, "General", Translate.DoTranslation("Initializing..."));
```
{% endcode %}

{% hint style="warning" %}
You must write the context correctly, as it is case-sensitive. Trying to report a progress on a non-existent context will simply do nothing.
{% endhint %}

## Full example code

This is the full example code that registers progress handlers for two contexts and reports the progress on them until the progress reaches 100%.

<pre class="language-csharp" data-title="TestProgressHandler.cs" data-line-numbers><code class="lang-csharp">using Terminaux.Colors.Themes.Colors;
using Terminaux.Writer.ConsoleWriters;
using System.Threading;
using Nitrocid.Base.Languages;
using Nitrocid.Base.Misc.Progress;

namespace Nitrocid.Base.Kernel.Debugging.Testing.Facades
{
    internal class TestProgressHandler : TestFacade
    {
        public override string TestName => LanguageTools.GetLocalized("NKS_KERNEL_DEBUGGING_TESTFACADES_TESTPROGRESSHANDLER_DESC");
        public override void Run()
        {
            int progress = 0;
<strong>            var handler = new ProgressHandler((num, text) =>
</strong><strong>                TextWriterColor.Write($"{num}% {text}", ThemeColorType.Progress)
</strong><strong>            , "General");
</strong><strong>            var handler2 = new ProgressHandler((num, text) =>
</strong><strong>                TextWriterColor.Write($"{num}% {text}", ThemeColorType.NeutralText)
</strong><strong>            , "Nongeneral");
</strong><strong>            ProgressManager.RegisterProgressHandler(handler);
</strong><strong>            ProgressManager.RegisterProgressHandler(handler2);
</strong>            while (progress != 100)
            {
                Thread.Sleep(100);
                progress += 1;
<strong>                ProgressManager.ReportProgress(progress, "General", LanguageTools.GetLocalized("NKS_KERNEL_DEBUGGING_TESTFACADES_TESTPROGRESSHANDLER_TEST"));
</strong><strong>                ProgressManager.ReportProgress(progress, "Nongeneral", LanguageTools.GetLocalized("NKS_KERNEL_DEBUGGING_TESTFACADES_TESTPROGRESSHANDLER_TEST"));
</strong>            }
<strong>            ProgressManager.UnregisterProgressHandler(handler);
</strong><strong>            ProgressManager.UnregisterProgressHandler(handler2);
</strong>        }
    }
}

</code></pre>
