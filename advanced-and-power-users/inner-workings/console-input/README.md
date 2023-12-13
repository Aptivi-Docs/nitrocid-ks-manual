---
description: When it comes to input, this is where the users provide their answers.
---

# 🖲 Console Input

You might have come across a chapter in making a console application that tells you to enter your name as a simplest course. Well, that's what this chapter is talking about; console inputs!

Nitrocid KS offers several ways of input. The simplest way is the `ReadLine()` function found in the Input class on the `KS.ConsoleBase.Inputs` namespace. It basically gives you a prompt and a chance to enter your input to the console, and the output will be returned by this function, which your mod uses.

{% hint style="info" %}
This feature is also available on Terminaux. Some of the features here might not get backported to Terminaux until the next version surfaces there.
{% endhint %}

Various features of the kernel, like the shell, use this function to get the user input, such as the entered command, and process it according to the logic. For example, `ShellManager.GetLine()` gets the entered command and compares the written command to the list of commands under the current shell type. Deep explanation about this topic is clearly out of scope, so if you want to get more information about how the shell commands are being processed, click on the below page:

{% content-ref url="../shell-structure/" %}
[shell-structure](../shell-structure/)
{% endcontent-ref %}

All the input functions that will be explained below use the input driver handled by the driver handler, which has its own manual page here:

{% content-ref url="../inner-essentials/kernel-drivers.md" %}
[kernel-drivers.md](../inner-essentials/kernel-drivers.md)
{% endcontent-ref %}

## Normal inputs

We'll cover the four types of input.

### Simple input

The simplest way to get an input from the user is to call the `ReadLine()` function found in the above class. Additionally, you can specify the input text and the default value to be used when nothing is entered.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static string ReadLine()
public static string ReadLine(string InputText)
public static string ReadLine(string InputText, string DefaultValue)
public static string ReadLine(string InputText, string DefaultValue, TermReaderSettings settings)
```
{% endcode %}

If you want the input to be wrapped into just one line, you can use the `ReadLineWrapped()` variants to achieve the same thing, but wrapped to one line instead of printing like normal. This is useful when you don't want text to overflow from the input box that may be one terminal cell long. Presentation system, for example, uses this technique to avoid overflowing.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static string ReadLineWrapped()
public static string ReadLineWrapped(string InputText)
public static string ReadLineWrapped(string InputText, string DefaultValue)
public static string ReadLineWrapped(string InputText, string DefaultValue, TermReaderSettings settings)
```
{% endcode %}

There is also an unsafe variant, called `ReadLineUnsafe()`, that allows you to get the console input straight from the user without waiting for the screensaver lock mode to exit.

```csharp
public static string ReadLineUnsafe(string InputText, string DefaultValue, bool OneLineWrap = false, TermReaderSettings settings = null)
```

{% hint style="warning" %}
Use `ReadLineUnsafe()` cautiously, because this variant doesn't wait for the lock mode to exit. Use `ReadLine()` or `ReadLineWrapped()` when possible.
{% endhint %}

{% hint style="info" %}
You can also use the `InputStyle` class to prompt the user for the input, but this is considered a legacy function, and may or may not be removed in the final release of 0.1.0. Use `ReadLine()` variants mentioned above when possible.
{% endhint %}

For passwords or any other sensitive data, you can make use of the `ReadLineNoInput()` functions to take advantage of hiding your written input when you're trying to enter your password or any other sensitive data.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static string ReadLineNoInput()
public static string ReadLineNoInput(char MaskChar)
public static string ReadLineNoInput(char MaskChar, TermReaderSettings settings)
```
{% endcode %}

There is also an unsafe variant, called ReadLineNoInputUnsafe(), that doesn't wait for the screensaver lock mode to exit.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static string ReadLineNoInputUnsafe()
public static string ReadLineNoInputUnsafe(char MaskChar)
public static string ReadLineNoInputUnsafe(TermReaderSettings settings)
public static string ReadLineNoInputUnsafe(char MaskChar, TermReaderSettings settings)
```
{% endcode %}

{% hint style="danger" %}
Be aware that even if the `NoInput` variants protect you from viewing the password or any other sensitive information, the output is still sent in plain text. Please encrypt this data as soon as you receive the output.
{% endhint %}

{% hint style="warning" %}
Use `ReadLineNoInputUnsafe()` cautiously, because this variant doesn't wait for the lock mode to exit. Use `ReadLineNoInput()` when possible.
{% endhint %}

{% hint style="info" %}
You can also use the `InputStyle` class to prompt the user for the password input, but this is considered a legacy function, and may or may not be removed in the final release of 0.1.0. Use `ReadLineNoInput()` variants mentioned above when possible.
{% endhint %}

### Key input

Now, for the key inputs, they only take one key and return the key information about what is the key that was pressed, what are the modifiers, and so on. This helps build interactive applications for the consoles and is cross-platform.

{% hint style="warning" %}
If you put a loop for this kind of input to handle a specific keypress, such as the Selection input type in which we're going to discuss later, you may experience missed keys when you're on the Windows system. This is because the timer resolution for the Windows systems is 15.6 milliseconds. While this can be changed to 1 millisecond, Microsoft have advised against using the [Windows API](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timebeginperiod) to reduce this resolution as it may cause issues with the Windows system performance.
{% endhint %}

To detect the keypress, use the `DetectKeypress()` function to get a key that is pressed.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static ConsoleKeyInfo DetectKeypress()
```
{% endcode %}

It returns a `ConsoleKeyInfo` instance, which you can find in this documentation link:

{% embed url="https://learn.microsoft.com/en-us/dotnet/api/system.consolekeyinfo?view=net-6.0" %}

If you want to have a timeout while the console is waiting for a key to be pressed, you may want to use the `ReadKeyTimeout()` function, indicating whether you need to intercept the key or not and the timeout in the `TimeSpan` format, which you can learn more about it here:

{% embed url="https://learn.microsoft.com/en-us/dotnet/api/system.timespan?view=net-6.0" %}

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static ConsoleKeyInfo ReadKeyTimeout(bool Intercept, TimeSpan Timeout)
```
{% endcode %}

There is also an unsafe version of the above function, called `ReadKeyTimeoutUnsafe()`, which doesn't wait for the screensaver lock mode to exit.

{% code title="Input.cs" lineNumbers="true" %}
```csharp
public static ConsoleKeyInfo ReadKeyTimeoutUnsafe(bool Intercept, TimeSpan Timeout)
```
{% endcode %}

{% hint style="warning" %}
Use `ReadKeyTimeoutUnsafe()` cautiously, because this variant doesn't wait for the lock mode to exit. Use `ReadKeyTimeout()` when possible.
{% endhint %}

### Choice input

If you want users to enter the choice number or the choice answer themselves, you can use this input method to prompt the user to write down the selection. For example, if you've given the user the following choices:

* `1) Authentication file`
* `2) Password`

They would have to write the number. This is possible by calling the below functions. However, there are several variants of the functions based on the type of the answer choices.

`PromptChoice()` function in the `ChoiceStyle` class helps you prompt the user for the choices easily. Here are several cases where the answer list would be of different types:

*   The easiest way to form a choice prompt is to use variants of the `PromptChoice()` function which take a string of answers, delimited by the slash (`/`). You can use the following variants:



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static string PromptChoice(string Question, string AnswersStr, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string AnswersStr, string[] AnswersTitles, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string AnswersStr, string[] AnswersTitles, string AlternateAnswersStr, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string AnswersStr, string[] AnswersTitles, string AlternateAnswersStr, string[] AlternateAnswersTitles, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    ```
    {% endcode %}
*   Another way to form a choice prompt is to use the variants of the `PromptChoice()` function which take an array of strings holding the answers.



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static string PromptChoice(string Question, string[] Answers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string[] Answers, string[] AnswersTitles, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string[] Answers, string[] AnswersTitles, string[] AlternateAnswers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, string[] Answers, string[] AnswersTitles, string[] AlternateAnswers, string[] AlternateAnswersTitles, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    ```
    {% endcode %}
*   Yet another way to form a choice prompt is to use the `List<InputChoiceInfo>` version of the `PromptChoice()` functions, which are defined below:



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static string PromptChoice(string Question, List<InputChoiceInfo> Answers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    public static string PromptChoice(string Question, List<InputChoiceInfo> Answers, List<InputChoiceInfo> AltAnswers, ChoiceOutputType OutputType = ChoiceOutputType.OneLine, bool PressEnter = false)
    ```
    {% endcode %}

Of course, there are types of the choice output, which allows you to change how the choices are presented. Currently, the above functions can render the choice list in the following ways:

* `ChoiceOutputType.OneLine`
* `ChoiceOutputType.TwoLines`
* `ChoiceOutputType.Modern`
* `ChoiceOutputType.Table`

{% hint style="info" %}
You can also use the infobox as a choice selection list. Use a desirable function from the `InfoBoxSelectionColor` class.

For choices that are three or less, you can use the `InfoBoxButtonsColor` class.
{% endhint %}

### Selection input

This kind of input is useful for those who prefer for the users to select any choice listed from the list of answers. This is useful for situations where we don't want the users to write down the choice number or title, or the choice list is too long.

Fortunately, `PromptSelection()` from `SelectionStyle` opens a full-screen choice selector which facilitates viewing of all the choices, as well as selecting a choice.

For example, the kernel settings application and the localization maker tool use this kind of input to allow the users to select their setting or their string without having to write down the whole thing.

Like `ChoiceInput`, the selection style contains these variants of functions:

*   The easiest way to form a selection prompt is to use variants of the `PromptSelection()` function which take a string of answers, delimited by the slash (`/`). You can use the following variants:



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static int PromptSelection(string Question, string AnswersStr, bool kiosk = false)
    public static int PromptSelection(string Question, string AnswersStr, string[] AnswersTitles, bool kiosk = false)
    public static int PromptSelection(string Question, string AnswersStr, string[] AnswersTitles, string AlternateAnswersStr, bool kiosk = false)
    public static int PromptSelection(string Question, string AnswersStr, string[] AnswersTitles, string AlternateAnswersStr, string[] AlternateAnswersTitles, bool kiosk = false)
    ```
    {% endcode %}
*   Another way to form a selection prompt is to use the variants of the `PromptSelection()` function which take an array of strings holding the answers.



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static int PromptSelection(string Question, string[] Answers, bool kiosk = false)
    public static int PromptSelection(string Question, string[] Answers, string[] AnswersTitles, bool kiosk = false)
    public static int PromptSelection(string Question, string[] Answers, string[] AnswersTitles, string[] AlternateAnswers, bool kiosk = false)
    public static int PromptSelection(string Question, string[] Answers, string[] AnswersTitles, string[] AlternateAnswers, string[] AlternateAnswersTitles, bool kiosk = false)
    ```
    {% endcode %}
*   Yet another way to form a selection prompt is to use the `List<InputChoiceInfo>` version of the `PromptSelection()` functions, which are defined below:



    {% code title="Input.cs" lineNumbers="true" %}
    ```csharp
    public static int PromptSelection(string Question, List<InputChoiceInfo> Answers, bool kiosk = false)
    public static int PromptSelection(string Question, List<InputChoiceInfo> Answers, List<InputChoiceInfo> AltAnswers, bool kiosk = false)
    ```
    {% endcode %}

{% hint style="info" %}
The `PromptSelection()` variants all return the selected choice number. If you're going to use this number to get an item from a list or an array, subtract this value from one to get an index.

If exit is requested by pressing the `Escape` key, this function will return `-1`, so make sure that you're checking it so that you don't run into out of bounds exceptions related to arrays or lists or other sorts of problems in the code that handle the choice.
{% endhint %}

In the selection style, these are the available controls:

* `Arrow up`: Moves the highlighted answer one answer up (selects the previous answer)
* `Arrow down`: Moves the highlighted answer one answer down (selects the next answer)
* `Home`: Moves the highlighted answer to the first answer (selects the first answer)
* `End`: Moves the highlighted answer to the last answer (selects the last answer)
* `Page Up`: Advances to the previous page
* `Page Down`: Advances to the next page
* `Enter`: Selects the highlighted answer
* `Escape`: Exits the selection and returns `-1`
* `Tab`: Opens an info box containing more information about the highlighted answer. This is useful if the information pane in the bottom didn't fit.

{% hint style="info" %}
You can also use the infobox as a choice selection list. Use a desirable function from the `InfoBoxSelectionColor` class.

For choices that are three or less, you can use the `InfoBoxButtonsColor` class.
{% endhint %}

## Other input types

If you want to explore other input types, click on the below links:

{% content-ref url="interactive-tui.md" %}
[interactive-tui.md](interactive-tui.md)
{% endcontent-ref %}

{% content-ref url="presentation-system.md" %}
[presentation-system.md](presentation-system.md)
{% endcontent-ref %}

Additionally, you can consult the Terminaux library documentation for more info:

{% content-ref url="https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/G0KrE9Uk2AiblqjWtpAo/" %}
[Terminaux - Manual](https://app.gitbook.com/o/fj052nYlsxW9IdL3bsZj/s/G0KrE9Uk2AiblqjWtpAo/)
{% endcontent-ref %}
