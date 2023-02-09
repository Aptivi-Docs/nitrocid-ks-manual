---
description: Debugging the kernel locally
---

# 🧬 Local Debugging

Locally debugging the kernel allows you to diagnose the kernel directly on the host computer. Debugging information from different kernel components are saved to a kernel debugging file, `kernelDbg-#.log`, where it is numbered depending on how many times the kernel is run.

## Structure

The structure of the local debugging log is as follows:

```
date time [level] (method - source:linenum): message
```

Each of these fields have their own values, as follows:

* `date`: The date of the event
* `time`: The time of the event
* `level`: One character error level, which is one of:
  * `T`: Trace verbose message
  * `D`: Debug verbose message
  * `I`: Informational message
  * `W`: Warning message
  * `E`: Error message
  * `F`: Fatal error message
* `method`: The method name in which the message was posted
* `source`: The source code file where the method is found
* `linenum`: The line number from the source file
* `message`: The message

## Debug your Mods

To debug your mods, they must call the debug functions in order for the kernel to acknowledge your message. There are useful functions listed below that may help you debug your routines in your mods.

### Normal Debugging

Calling the debug function below will post your debug message to the kernel debugger normally. There's a function for you to call below:

```csharp
public static void WriteDebug(DebugLevel Level, string text, params object[] vars)
```

Found in the `DebugWriter` module under the `KS.Kernel.Debugging` namespace.

### Conditional Debugging

Calling the debug function below will post your debug message to the kernel debugger if the condition that you've set within the function is satisfied. There's a function for you to call below:

```csharp
public static void WriteDebugConditional(bool Condition, DebugLevel Level, string text, params object[] vars)
```

Found in the `DebugWriter` module under the `KS.Kernel.Debugging` namespace.

### Stack Trace Debugging

Calling the debug function below will post the stack trace of an exception, including its inner exceptions, to the kernel debugger. There's a function for you to call below:

```csharp
public static void WriteDebugStackTrace(Exception Ex)
```

Found in the `DebugWriter` module under the `KS.Kernel.Debugging` namespace.

### Stack Trace Conditional Debugging

Calling the debug function below will post the stack trace of an exception, including its inner exceptions, to the kernel debugger if the condition that you've set within the function is satisfied. There's a function for you to call below:

```csharp
public static void WriteDebugStackTraceConditional(bool Condition, Exception Ex)
```

Found in the `DebugWriter` module under the `KS.Kernel.Debugging` namespace.
