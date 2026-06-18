---
description: Each of the settings contain their own format
icon: screwdriver
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/kernel-settings/settings-format
---

# Settings Format

This page specifies all the possible configuration formats.

***

## <mark style="color:$primary;">Kernel Configuration Entries</mark>

The most basic pseudo-representation of the settings entry file is printed below to illustrate the concept:

```json
[
    {
        "Name": "SectionName",
        "Desc": "Description of the section, usually a short one.",
        "DisplayAs": "Section name to be displayed in the app",
        "Keys": [
            {
                "Name": "Key name to be displayed in the app",
                "Type": "SType",
                "Variable": "VarName",
                "Description": "Description of the key, usually a short one."
            }
        ]
    }
]
```

Basically, all of the settings entry files start with an array containing one or more of the sections under the selected name for reference.

<details>

<summary>Configuration section entries</summary>

Each section contains these necessary entries:

<table><thead><tr><th width="120">Variable</th><th width="400.333251953125">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Name</code></td><td>This variable holds the short section name.</td><td><strong>string</strong></td></tr><tr><td><code>Desc</code></td><td>This variable holds the description of the section to be displayed in the bottom of the application.</td><td><strong>string, localizable</strong></td></tr><tr><td><code>DisplayAs</code></td><td>This variable holds the text to display in the settings application.</td><td><strong>string, localizable</strong></td></tr><tr><td><code>Keys</code></td><td>This variable holds the settings entries.</td><td><strong>array</strong></td></tr></tbody></table>

</details>

<details>

<summary>Configuration key entries</summary>

In the `Keys` variable, it contains an array of objects containing the settings entry information. They get used by the settings application to determine what to do when getting and setting the variable value.

The entry information is detailed below (in general case):

<table><thead><tr><th width="120">Variable</th><th width="400.333251953125">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Name</code></td><td>This contains the key name to be displayed by the settings application.</td><td><strong>string, localizable</strong></td></tr><tr><td><code>Type</code></td><td>The type of a variable, depending on the variable and on the purpose.</td><td><strong>string</strong></td></tr><tr><td><code>Variable</code></td><td>The variable to get and to set the values from/to.</td><td><strong>string</strong></td></tr><tr><td><code>Description</code></td><td>The description of the entry, to describe what is the purpose.</td><td><strong>string, localizable</strong></td></tr></tbody></table>

</details>

<details>

<summary>Optional key entry variables</summary>

The variables that can be omitted are specified below:

<table><thead><tr><th width="200.66668701171875">Variable</th><th width="330">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Masked</code></td><td>Specifies whether the string is a secret or not (shows as asterisks when editing).</td><td><strong>boolean</strong></td></tr><tr><td><code>IsEnumeration</code></td><td>If the variable is an enumeration, set to <code>true</code>.</td><td><strong>boolean</strong></td></tr><tr><td><code>IsValuePath</code></td><td>If the value takes a path, then <code>true</code>.</td><td><strong>boolean</strong></td></tr><tr><td><code>IsPathCurrentPath</code></td><td>If the value takes a relative path, then <code>true</code> to neutralize the input path to the current path.</td><td><strong>boolean</strong></td></tr><tr><td><code>UnsupportedPlatforms</code></td><td>The value is unsupported on one or more of the host platforms. The settings application won't display this value on an unsupported platform.</td><td><strong>array</strong> of <strong>strings</strong>, one of <code>"windows"</code>, <code>"unix"</code>, <code>"macos"</code></td></tr><tr><td><code>ValuePathType</code></td><td>The path type to use for values. <code>IsPathCurrentPath</code> must be <code>false</code>.</td><td><strong>string</strong></td></tr></tbody></table>

</details>

***

## <mark style="color:$primary;">Requirements for key types</mark>

In special cases, each type might require different variables to be set before the settings application knows what to do.

These types are listed below:

* `SBoolean`
* `SInt`
* `SString`
* `SSelection`
* `SList`
* `SColor`
* `SChar`
* `SIntSlider`
* `SDouble`
* `SPreset`
* `SFiglet`
* `SMultivar`

Only the types that require additional configuration are listed below. The below variables must be set to work with these types:

<details>

<summary><code>SSelection</code></summary>

This type is a selection from the list of the values that a function or an enumeration returns.

<mark style="color:$primary;">**Case 1: (**</mark><mark style="color:$primary;">**`IsEnumeration`**</mark> <mark style="color:$primary;">**is**</mark> <mark style="color:$primary;">**`false`**</mark><mark style="color:$primary;">**)**</mark>

The format is as below:

```json
{
    "IsEnumeration": false,
    "SelectionFunctionName": "FunctionThatReturnsAList",
    "SelectionFunctionType": "TypeThatImplementsTheFunction",
    "SelectionFunctionArgs": [
        {
            "ArgType": "System.Boolean",
            "ArgValue": "False"
        }
    ],
    "SelectionFallback": [ "Fallback 1" ]
}
```

If the target listing is not an enumeration, the list can be obtained using a function that returns a list of possible options that can be set here.

<table><thead><tr><th width="209.33331298828125">Variable</th><th width="350">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>SelectionFunctionName</code></td><td>The function within the below specified type that returns the list. It must contain no arguments.</td><td><strong>string</strong></td></tr><tr><td><code>SelectionFunctionType</code></td><td>The type containing the function above (must be a fully-qualified type name).</td><td><strong>string</strong></td></tr><tr><td><code>SelectionFunctionArgs</code></td><td>An array of arguments to be passed to the function (if omitted, nothing is passed to the function).</td><td><strong>object</strong></td></tr><tr><td><code>SelectionFallback</code></td><td>An array of the fallback values in case the function fails.</td><td><strong>array</strong></td></tr></tbody></table>

`SelectionFunctionArgs` is an object that contains the two keys:

<table><thead><tr><th width="109.99993896484375">Variable</th><th width="447.3333740234375">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>ArgType</code></td><td>A fully qualified name of a target type (must be simple types, such as <code>System.String</code>).</td><td><strong>string</strong></td></tr><tr><td><code>ArgValue</code></td><td>A valid value that can be converted to the target type.</td><td><strong>string</strong></td></tr></tbody></table>

{% hint style="info" %}
In the `SelectionFunctionArgs` value, please make sure that you pass the correct number of parameters in their correct order and in their correct types.
{% endhint %}

<mark style="color:$primary;">**Case 2: (**</mark><mark style="color:$primary;">**`IsEnumeration`**</mark> <mark style="color:$primary;">**is**</mark> <mark style="color:$primary;">**`true`**</mark><mark style="color:$primary;">**)**</mark>

The format is as below:

```json
{
    "IsEnumeration": true,
    "EnumerationInternal": false,
    "Enumeration": "Namespace.Enum",
    "EnumerationAssembly": "Assembly",
    "EnumerationZeroBased": false
}
```

If the target listing is an enumeration, the list can be obtained immediately with a list of possible options that can be set here.

<table><thead><tr><th width="209.33331298828125">Variable</th><th width="350">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>EnumerationInternal</code></td><td>Specifies whether the enumeration is found within the kernel or within an external assembly.</td><td><strong>boolean</strong></td></tr><tr><td><code>Enumeration</code></td><td><p>The fully qualified name of the enumeration, including the whole namespace.</p><p>If internal, <code>Nitrocid.</code> can be omitted.</p><p>Enumerations inside the static classes must be appended with the plus sign, for example, <code>ConsoleBase.Inputs.Styles.ChoiceStyle+ChoiceOutputType</code>.</p></td><td><strong>string</strong></td></tr><tr><td><code>EnumerationAssembly</code></td><td>An assembly name containing the enumeration. It can be omitted if enumeration is internal.</td><td><strong>string</strong></td></tr><tr><td><code>EnumerationZeroBased</code></td><td>If the enumeration is zero-based, then true. Otherwise, the enumeration is assumed to start from one.</td><td><strong>boolean</strong></td></tr></tbody></table>

</details>

<details>

<summary><code>SList</code></summary>

This type allows lists to be made in kernel settings. It contains list of configured values.

<mark style="color:$primary;">**Case 1 (dynamic delimiter)**</mark>

The format is as below:

```json
{
    "SelectionFunctionName": "GetPathList",
    "SelectionFunctionType": "Filesystem",
    "DelimiterVariable": "PathLookupDelimiter"
}
```

The target list is always a parameterless function that always returns a list that is found under a Nitrocid type. The list type takes a string and splits it using the specified delimiter found in a variable.

<table><thead><tr><th width="209.33331298828125">Variable</th><th width="350">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>SelectionFunctionName</code></td><td>The function within the below specified type that returns the list. It must contain no arguments.</td><td><strong>string</strong></td></tr><tr><td><code>SelectionFunctionType</code></td><td>The type containing the function above.</td><td><strong>string</strong></td></tr><tr><td><code>DelimiterVariable</code></td><td>The variable containing the delimiter character.</td><td><strong>string</strong></td></tr><tr><td><code>DelimiterVariableType</code></td><td>The type containing the delimiter variable name (must be a fully-qualified type name)</td><td><strong>string</strong></td></tr></tbody></table>

<mark style="color:$primary;">**Case 2 (hardcoded delimiter)**</mark>

The format is as below:

```json
{
    "SelectionFunctionName": "GetPathList",
    "SelectionFunctionType": "Filesystem",
    "Delimiter": ";"
}
```

The target list is always a parameterless function that always returns a list that is found under a Nitrocid KS type. The list type takes a string and splits it using the specified delimiter.

<table><thead><tr><th width="209.33331298828125">Variable</th><th width="350">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>SelectionFunctionName</code></td><td>The function within the below specified type that returns the list. It must contain no arguments.</td><td><strong>string</strong></td></tr><tr><td><code>SelectionFunctionType</code></td><td>The type containing the function above.</td><td><strong>string</strong></td></tr><tr><td><code>Delimiter</code></td><td>The delimiter character.</td><td><strong>string</strong></td></tr></tbody></table>

</details>

<details>

<summary><code>SPreset</code></summary>

This type is a shell preset that is treated as a string in the kernel configuration file, but it's actually set by the shell preset manager.

<mark style="color:$primary;">**General case**</mark>

The format is as below:

```json
{
    "ShellType": "Shell"
}
```

It provides only one variable, `ShellType`, that specifies the shell type for listing all the presets. It delegates the listing functions to `PromptPresetManager.PromptForPresets()` function with the shell type in the `Nitrocid.Shell.Prompts` namespace.

<table><thead><tr><th width="209.33331298828125">Variable</th><th width="350">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>SelectionFunctionName</code></td><td>The function within the below specified type that returns the list. It must contain no arguments.</td><td><strong>string</strong></td></tr></tbody></table>

</details>

<details>

<summary><code>SIntSlider</code></summary>

This type is for integer values which are limited. They're surrounded between the minimum number and the maximum number, which can be represented like this (`x` is a value):

<p align="center"><span class="math">N_{min} &#x3C; x &#x3C; N_{max}</span></p>

**General case**

The format is as below:

```json
{
    "MinimumValue": 0,
    "MaximumValue": 10
}
```

There are two variables that must be set. One for the minimum value and one for the maximum value.

<table><thead><tr><th width="139.99993896484375">Variable</th><th width="409.3333740234375">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>MinimumValue</code></td><td>The minimum value to be set.</td><td><strong>integer</strong></td></tr><tr><td><code>MaximumValue</code></td><td>The maximum value to be set.</td><td><strong>integer</strong></td></tr></tbody></table>

</details>

<details>

<summary><code>SMultivar</code></summary>

This type is to group multiple settings entries, which are indicated in an array value of the `Variables` key in the entries JSON file. The format is as below:

```json
{
    "Name": "Kernel color schemes",
    "Type": "SMultivar",
    "Description": "This allows you to set multiple kernel color schemes",
    "Variables": [
        {
            "Name": "User Name Shell Color",
            "Type": "SColor",
            "Variable": "UserNameShellColor"
        },
        (...)
    ]
}
```

{% hint style="info" %}
You can nest the `SMultivar` entries, since the `Variables` value gets deserialized into an array of the settings entries instance used internally, and the settings application takes this into account.
{% endhint %}

</details>

***

## <mark style="color:$primary;">Other configuration types</mark>

There are other configuration types that different parts of Nitrocid uses, such as user configuration.

<details>

<summary>User Configuration</summary>

The kernel makes a user configuration entry for each new user created either by the `adduser` command or by the call of the `UserManagement.InitializeUser()` function in the `Nitrocid.Users` namespace under the name of `Users.json` found in the kernel configuration directory.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
[
  {
    "Username": "name",
    "FullName": "Full Name",
    "PreferredLanguage": "",
    "Groups": [],
    "Password": "encrypted password",
    "Flags": 1,
    "Permissions": [],
    "CustomSettings": {
      "key1": [
        "value1"
      ],
      (...)
    }
  }
]
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="180.6666259765625">Variable</th><th width="330">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Username</code></td><td>Stores the username.</td><td><strong>string</strong></td></tr><tr><td><code>FullName</code></td><td>Stores the full name.</td><td><strong>string</strong></td></tr><tr><td><code>PreferredLanguage</code></td><td>Stores the preferred user language in three-letter language name format. Can be left blank to use the kernel-wide language.</td><td><strong>string</strong></td></tr><tr><td><code>Groups</code></td><td>What groups the user is in?</td><td><strong>array</strong> of <strong>string</strong></td></tr><tr><td><code>Password</code></td><td>Stores the password.</td><td><strong>string (SHA256)</strong></td></tr><tr><td><code>Flags</code></td><td>Specifies a number representing the flags.</td><td><strong>integer</strong></td></tr><tr><td><code>Permissions</code></td><td>Stores the array of permissions found under <a href="https://github.com/Aptivi/Kernel-Simulator/blob/master/public/Kernel%20Simulator/Users/Permissions/PermissionTypes.cs">the permission list, <code>PermissionTypes</code></a>.</td><td><strong>array</strong> of <strong>string</strong></td></tr><tr><td><code>CustomSettings</code></td><td>Specifies the customized settings entries</td><td><strong>array</strong> of <strong>properties</strong></td></tr></tbody></table>

The type of `Flags` is an **integer** that can be a sum of the following flags:

* `1`: Administrator
* `2`: Anonymous
* `4`: Disabled

</details>

<details>

<summary>Group configuration</summary>

The kernel also supports user groups created either by the `addgroup` command or by the call of the `GroupManagement.AddGroup()` function in the `Nitrocid.Users.Groups` namespace under the name of `UserGroups.json` found in the kernel configuration directory.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
[
  {
    "GroupName": "testGroup",
    "Permissions": []
  }
]
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="180.6666259765625">Variable</th><th width="330">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>GroupName</code></td><td>The name of the group.</td><td><strong>string</strong></td></tr><tr><td><code>Permissions</code></td><td>Stores the array of permissions found under <a href="https://github.com/Aptivi/Kernel-Simulator/blob/master/public/Kernel%20Simulator/Users/Permissions/PermissionTypes.cs">the permission list, <code>PermissionTypes</code></a>.</td><td><strong>array</strong> of <strong>strings</strong></td></tr></tbody></table>

</details>

<details>

<summary>Alias configuration</summary>

The kernel makes an alias configuration entry for each new alias created either by the `alias` command or by the call of the `AliasManager.ManageAlias()` function in the `Nitrocid.Shell.ShellBase.Aliases` namespace under the name of `Aliases.json` found in the kernel configuration directory.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
[
  {
    "Alias": "alias",
    "Command": "cmd",
    "Type": "ShellType"
  }
]
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="180.6666259765625">Variable</th><th width="330">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Alias</code></td><td>Stores the alias.</td><td><strong>string</strong></td></tr><tr><td><code>Command</code></td><td>Stores the target command.</td><td><strong>string</strong></td></tr><tr><td><code>Type</code></td><td>The shell type</td><td><strong>boolean</strong></td></tr></tbody></table>

</details>

<details>

<summary>Debug Device Configuration</summary>

The kernel makes a debug device configuration entry for each new device connected to the remote debugger under the name of `DebugDevicesNames.json` found in the kernel configuration directory.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
[
  {
    "Address": "192.168.1.100",
    "Name": "device",
    "Blocked": false,
    "MuteLogs": false,
    "ChatHistory": []
  }
]
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="180.6666259765625">Variable</th><th width="330">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>Address</code></td><td>Stores the device address.</td><td><strong>string</strong></td></tr><tr><td><code>Name</code></td><td>Stores the name of the remote debug device.</td><td><strong>string</strong></td></tr><tr><td><code>Blocked</code></td><td>Whether the device is banned or not.</td><td><strong>boolean</strong></td></tr><tr><td><code>MuteLogs</code></td><td>Whether to mute the kernel debug logs or not. Useful for conversations.</td><td><strong>boolean</strong></td></tr><tr><td><code>ChatHistory</code></td><td>Recent chat history</td><td><strong>array</strong> of <strong>strings</strong></td></tr></tbody></table>

</details>

<details>

<summary>Event configuration</summary>

The kernel makes an event file for each event made in the `KSEvents` folder by `calendar event saveall`.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
{
    "EventDate": "2023-12-18T00:00:00",
    "EventTitle": "Test",
    "IsYearly": false,
    "StartMonth": 1,
    "StartDay": 1,
    "EndMonth": 1,
    "EndDay": 1,
    "Calendar": "Gregorian"
}
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="119.99993896484375">Variable</th><th width="438">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>EventDate</code></td><td>Stores the date (and time) of the event.</td><td><strong>date</strong></td></tr><tr><td><code>EventTitle</code></td><td>The event title that's usually what's happening on the specified date.</td><td><strong>string</strong></td></tr><tr><td><code>IsYearly</code></td><td>Whether or not this event is a yearly event.</td><td><strong>boolean</strong></td></tr><tr><td><code>StartMonth</code></td><td>For yearly events, specifies the start month.</td><td><strong>integer</strong></td></tr><tr><td><code>StartDay</code></td><td>For yearly events, specifies the start day.</td><td><strong>integer</strong></td></tr><tr><td><code>EndMonth</code></td><td>For yearly events, specifies the end month.</td><td><strong>integer</strong></td></tr><tr><td><code>EndDay</code></td><td>For yearly events, specifies the end day.</td><td><strong>integer</strong></td></tr><tr><td><code>Calendar</code></td><td>The calendar used while parsing the event date.</td><td><strong>string</strong></td></tr></tbody></table>

</details>

<details>

<summary>Reminder configuration</summary>

The kernel makes a reminder file for each reminder made in the `KSReminders` folder by `calendar reminder saveall`.

#### <mark style="color:$primary;">Format</mark>

The format of the file looks like this:

```json
{
    "ReminderDate": "2023-12-17T16:00:00",
    "ReminderTitle": "W2",
    "ReminderImportance": 1
}
```

#### <mark style="color:$primary;">Explanation</mark>

Let's explain each key one by one:

<table><thead><tr><th width="180">Variable</th><th width="369.6666259765625">Description</th><th>Type</th></tr></thead><tbody><tr><td><code>ReminderDate</code></td><td>Stores the date (and time) of the reminder.</td><td><strong>date</strong></td></tr><tr><td><code>ReminderTitle</code></td><td>The reminder title that's usually what you're reminded of.</td><td><strong>string</strong></td></tr><tr><td><code>ReminderImportance</code></td><td>The reminder importance shows how important is the thing that you're reminded of.</td><td><strong>string</strong></td></tr></tbody></table>

where `ReminderImportance` is one of `Low`, `Medium`, or `High`.

</details>

<details>

<summary>MAL and MOTD configuration</summary>

The configuration files for the message of the day before login (MOTD) and after login (MAL) are found under the kernel configuration directory. They are just plain-text files with the kernel placeholder support found in the below page linked to you below:

<a href="../inner-essentials/kernel-placeholders.md" class="button primary">Kernel placeholders</a>

Both of these files are read every time the kernel log-in handler starts. The functions that are responsible for loading such info are both the `ReadMotd()` and the `ReadMal()` functions found under their respective namespaces `Nitrocid.Misc.Probers.Motd` and `Nitrocid.Misc.Probers.Mal`.

Changes to both files are done by the `SetMotd()` and the `SetMal()` functions under the same namespace. They're invoked either manually or by the usage of the `chmotd` and the `chmal` commands in the main shell.

</details>
