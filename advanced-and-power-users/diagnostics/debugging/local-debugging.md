---
icon: bugs
description: Debugging the kernel locally
---

# Local Debugging

Locally debugging the kernel allows you to diagnose the kernel directly on the host computer. Debugging information from different kernel components are saved to a kernel debugging log file. Aptivestigate uses the following paths to log the events:

* Windows: `%LOCALAPPDATA%/Aptivi/Logs`
* Unix: `~/.config/Aptivi/Logs`

{% hint style="info" %}
The `Logs` directory doesn't necessarily contain files that pertain to what Nitrocid logs, but you can distinguish them using the `Nitrocid` name directly after the `log_` prefix (e.g. `log_Nitrocid_202412300947526611103_1b0264b4-856e-4024-b822-bf384765ae4e.txt`).
{% endhint %}

## Structure

The structure of the local debugging log is like the below picture:

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Every line in the local debug logs follow the below structure (if debug information is available):

```
date time offset [level] (method - source:linenum): message
```

* `date`: The date of the event
* `time`: The time of the event
* `offset`: The time zone offset of the event
* `level`: Logging level, which is one of:
  * `T`: Trace verbose message (as `DBG`)
  * `D`: Debug verbose message (as `DBG`)
  * `I`: Informational message (as `INF`)
  * `W`: Warning message (as `WRN`)
  * `E`: Error message (as `ERR`)
  * `F`: Fatal error message  (as `FTL`)
* `method`: The method name in which the message was posted
* `source`: The source code file where the method is found
* `linenum`: The line number from the source file
* `message`: The message

## Debug your Mods

To debug your mods, they must call the debug functions in order for the kernel to acknowledge your message. There are useful functions listed below that may help you debug your routines in your mods.

{% hint style="info" %}
You can also use the Output window if you've built Nitrocid KS with `VSDEBUG` compiler constant, but it has severe performance repercussions.
{% endhint %}

### Normal Debugging

Calling the debug function below will post your debug message to the kernel debugger normally. There's a function for you to call below:

```csharp
public static void WriteDebug(DebugLevel Level, string text, [CallerMemberName] string memberName = "", [CallerLineNumber] int memberLine = 0, [CallerFilePath] string memberPath = "", object?[]? vars = null)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.

### Conditional Debugging

Calling the debug function below will post your debug message to the kernel debugger if the condition that you've set within the function is satisfied. There's a function for you to call below:

```csharp
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, [CallerMemberName] string memberName = "", [CallerLineNumber] int memberLine = 0, [CallerFilePath] string memberPath = "", object?[]? vars = null)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.

### Privacy-aware Debugging

Calling the debug function below will post your debug message to the kernel debugger normally. However, it also filters every variable you've selected to be censored in the debug log. For example, if you provide two variables (A, B) and B contains sensitive info, you may want to create an array of indexes which holds B's index (in this case, 1) when calling the below function.

```csharp
public static void WriteDebugPrivacy(DebugLevel Level, string text, int[] SecureVarIndexes, [CallerMemberName] string memberName = "", [CallerLineNumber] int memberLine = 0, [CallerFilePath] string memberPath = "", object?[]? vars = null)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.

### Stack Trace Debugging

Calling the debug function below will post the stack trace of an exception, including its inner exceptions, to the kernel debugger. There's a function for you to call below:

```csharp
public static void WriteDebugStackTrace(Exception? Ex)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.

### Stack Trace Conditional Debugging

Calling the debug function below will post the stack trace of an exception, including its inner exceptions, to the kernel debugger if the condition that you've set within the function is satisfied. There's a function for you to call below:

```csharp
public static void WriteDebugStackTraceConditional(bool Condition, Exception? Ex)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.

### Log-Only Debugging

Calling the debug function below will post your debug message to the kernel debugger without relaying it to all remote debug devices. There's a function for you to call below:

```csharp
public static void WriteDebugLogOnly(DebugLevel Level, string text, [CallerMemberName] string memberName = "", [CallerLineNumber] int memberLine = 0, [CallerFilePath] string memberPath = "", object?[]? vars = null)
```

Found in the `DebugWriter` module under the `Nitrocid.Kernel.Debugging` namespace.
