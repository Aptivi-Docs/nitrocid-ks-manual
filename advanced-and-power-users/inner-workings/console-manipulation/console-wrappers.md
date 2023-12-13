---
description: Make your console more powerful
---

# 🧩 Console Wrappers

Nitrocid KS currently provides you with a console wrapper that allows you to wrap the console functions to the console driver. That driver is itself a delegate to the actual console driver functions, which you can learn more about by clicking on the below page:

{% content-ref url="../inner-essentials/kernel-drivers.md" %}
[kernel-drivers.md](../inner-essentials/kernel-drivers.md)
{% endcontent-ref %}

The console wrappers allow you to call compatible console functions to simplify the syntax of calling the console driver functions, which are available below:

* `CursorLeft`
  * The cursor left position
* `CursorTop`
  * The cursor top position
* `WindowWidth`
  * The console window width (columns)
* `WindowHeight`
  * The console window height (rows)
* `WindowTop`
  * The console window topmost position
* `BufferWidth`
  * The console buffer width (columns)
* `BufferHeight`
  * The console buffer height (rows)
* `CursorVisible`
  * The console cursor visibility
* `OutputEncoding`
  * The console output encoding (Windows only)
* `InputEncoding`
  * The console input encoding (Windows only)
* `TreatCtrlCAsInput`
  * Whether to treat CTRL + C as input or not
* `KeyAvailable`
  * Whether a key is pressed or not
* `Clear()`
  * Clears the console screen, optionally filling it with the selected background
* `SetCursorPosition()`
  * Sets the cursor position
* `ResetColor()`
  * Resets the console colors
* `OpenStandardInput()`
  * Opens the standard input stream
* `OpenStandardOutput()`
  * Opens the standard output stream
* `OpenStandardError()`
  * Opens the standard error stream
* `SetOut()`
  * Sets the console output stream
* `Beep()`
  * Beeps the console
* `ReadKey()`
  * Reads a key if it is not available or gets a key if it is available
* `Write()`
  * Writes text to the console
* `WriteLine()`
  * Writes text to the console with a trailing newline

More information about console wrappers can be found in the Terminaux manual.

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-wrapper" %}
[Console Wrapper](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/console-tools/console-wrapper)
{% endcontent-ref %}
