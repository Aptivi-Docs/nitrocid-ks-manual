---
description: Talks about shell scripting and how it works
---

# 📜 Shell Scripting

UESH shell contains scripting support. The shell scripts have the `.uesh` extension containing a subset of UESH commands inside it. A simple UESH script containing a command that sets a UESH variable is as follows:

```
set $hellotext Hello
echo $hellotext
```

## Script parser

When this script file is executed, the UESH script parser skims the file for any possible `$variables` and initializes them with their default values using the `UESHVariables.InitializeVariable` function.

The parser then attempts to skim the script lines for all the variables, and replaces them with the value. The parser also attempts to parse the script argument placeholders, defined with `{num}`; which `num` is the argument number, in case the ︎user executed the script with the arguments. For example, this script prints the first argument:

```
echo {0}
```

As soon as the parsing is done, the final line gets executed by the `GetLine()` command.

## Variables

UESH provides the variable facility, which holds the variable as a key and the variable value as a value. Each variable starts with the dollar sign like `$var`, regardless of the platform.

When a variable gets initialized by `InitializeVariable()`, the variable name gets sanitized (`SanitizeVariableName()`) by appending the dollar sign in front of the variable name, which then gets initialized with the empty value.

The variable can be read from and written to by these respective functions: `GetVariable()` and `SetVariable()`. These can be used by your mods. Additionally, an array of values can be initialized with one variable by `SetVariables()` to initialize `$var[n]` variables, which:

* `var`: A variable name
* `n`: How many values are there (count from 0)

When the kernel starts up, `ConvertSystemEnvironmentVariables()` queries the operating system for environment variables and sets them one by one to the UESH variable store. Its list can be obtained by the `GetVariables()` function.

{% hint style="warning" %}
Additionally, the variables can be uninitialized by the `RemoveVariable()` function. When the target variable is removed, it has to be re-initialized before it can be used again.
{% endhint %}

## Conditions

No scripting is complete with conditions, which control the execution of the command. These conditions are currently available to be used: (`<value>` can either be a constant or a UESH `$variable`)

* `eq`: The value is equal to the value
  * Usage: `<value> eq <value>`
* `neq`: The value is not equal to the value
  * Usage: `<value> neq <value>`
* `les`: The number is less than another number
  * Usage: `<value> les <value>`
* `lesoreq`: The number is less than or equal to another number
  * Usage: `<value> lesoreq <value>`
* `gre`: The number is greater than another number
  * Usage: `<value> gre <value>`
* `greoreq`: The number is greater than or equal to another number
  * Usage: `<value> greoreq <value>`
* `fileex`: The file exists
  * Usage: `fileex <value>`
* `filenex`: The file doesn't exist
  * Usage: `filenex <value>`
* `direx`: The directory exists
  * Usage: `direx <value>`
* `dirnex`: The directory doesn't exist
  * Usage: `dirnex <value>`
* `has`: The specified string contains a substring
  * Usage: `<value> has <value>`
* `hasno`: The specified string doesn't contain a substring
  * Usage: `<value> hasno <value>`
* `ispath`: The specified path is valid
  * Usage: `<value> ispath`
* `isnotpath`: The specified path is invalid
  * Usage: `<value> isnotpath`
* `isfname`: The specified file name is valid
  * Usage: `<value> isfname`
* `isnotfname`: The specified file name is invalid
  * Usage: `<value> isnotfname`
* `sane`: The hash matches the expected hash
  * Usage: `<value> <value> sane`
* `insane`: The hash doesn't match the expected hash
  * Usage: `<value> <value> insane`
* `fsane`: The file hash matches the expected hash
  * Usage: `<value> <value> fsane`
* `finsane`: The file hash doesn't match the expected hash
  * Usage: `<value> <value> finsane`

The conditions all have their base condition class and their interface to be implemented like below:

```csharp
public class YourCondition : BaseCondition, ICondition
```

Basically, you must override all the variables, where:

* `ConditionName`: A condition name without spaces to be included in the expression

```csharp
public override string ConditionName => "dirnex";
```

* `ConditionPosition`: Which word number starting from 1 should the expression be found?

```csharp
public override int ConditionPosition { get; } = 1;
```

* `ConditionRequiredArguments`: How many arguments are required? Starting from 1.

```csharp
public override int ConditionRequiredArguments { get; } = 2;
```

Choose one of the two method overloads to override, depending on your condition:

* `IsConditionSatisfied(string FirstVariable, string SecondVariable)`
  * This function checks the two variables to see if they satisfy a condition

```csharp
public override bool IsConditionSatisfied(string FirstVariable, string SecondVariable)
```

* `IsConditionSatisfied(string[] Variables)`
  * This function checks any number of variables to see if they satisfy a condition

```csharp
public override bool IsConditionSatisfied(string[] Variables)
```

{% hint style="warning" %}
We currently don't support installing the custom condition, but we'll add support for it soon.
{% endhint %}

You can call `ConditionSatisfied()` to test any built-in or custom condition. Give it any expression and test it with `true`.

{% hint style="warning" %}
The `if` command in the UESH shell is a major contributor to the condition system, though it can be changed in the future.
{% endhint %}

### Conditional blocks and Loops

The conditional blocks and loops are one of the most essential scripting features that control the script flow based on the conditions and conditional loops. These are currently supported:

* `if <condition>`
* `while <condition>`
* `until <condition>`

After the script parser detects one of these, it checks for the new block stack in the next line, like this:

```
if $test2 eq y
|set $test3 n
```

{% hint style="danger" %}
The new block stack must be defined with one extra `|` character directly after lines that start with one of the above conditional block statements. Otherwise, parsing will fail.
{% endhint %}

If defined correctly, the script parser walks through the commands defined in the new stack. However, if the condition is not satisfied, the whole block stack for the first conditional block that doesn't satisfy the condition will be skipped and the parser will continue executing commands that are defined in the current stack. For example, consider this:

{% code lineNumbers="true" %}
```
choice -m $test2 y/n "Found any bugs?"
if $test2 eq y
|set $test3 n
|until $test3 eq y
||choice -m $test3 y/n "Exit?"
||echo Current: $test3
|echo out of until
echo out of if
```
{% endcode %}

This script first checks to see if the user has answered `y` in the first line. The following will happen:

* If the user answered `y`, the script parser enters the new stack defined by the `if` condition in line 2.
* If the user answered `n`, the script parser skips the new stack defined by the `if` condition and continues parsing the commands from line 8.

`while` and `until` blocks require the new stack to be defined. In addition to this, the script parser checks to see if the condition is no longer satisfied after the stack that these blocks defined.

* If the condition is satisfied, the commands after the `while` or `until` blocks get executed.
* If the condition is not satisfied, the commands after the `while` or `until` blocks get skipped and the script parser continues parsing the commands.
