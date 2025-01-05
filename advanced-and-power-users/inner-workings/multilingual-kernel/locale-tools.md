---
description: What do you want to do with the locales?
icon: earth-americas
---

# Locale Tools

The locale tools can be found in a separate application, `Nitrocid.Locales`. It's a command-line tool that allows you to do the following:

* Trim unused languages found in the Nitrocid source code (`trim`)
* Remove unused strings found in the Nitrocid source code (`clean`)
* Check for unlocalized strings in the Nitrocid source code (`check`)
* Generate localization info from either the Nitrocid source code or the custom string list (`generate`)

The first three functions are left intentionally undocumented, as they're meant to be operated only when located at the build output of the Nitrocid source code.

{% hint style="info" %}
You can use the help argument to get a list of available functions, and use this argument against a function that you need to get more information about said argument.
{% endhint %}

## Locale Generator

The generator part generates the JSON file for the built-in kernel languages and the custom languages. It allows you to generate the JSON file usable for the kernel.

### Metadata

Each copy of Nitrocid KS provides you two placeholder folders, `CustomLanguages` and `Translations`. Each of these folders must contain the metadata JSON file, `Metadata.json`, which is detailed below: (The `codepage` variable can be omitted)

#### For normal languages

```json
[
    {
        "three": "lng",
        "name": "Language",
        "transliterable": false,
        "codepage": 65001,
        "country": "United Kingdom"
    }
]
```

#### For transliterable languages

Both the language entries are required.

```json
[
    {
        "three": "lng",
        "name": "Language",
        "transliterable": true,
        "codepage": 65001,
        "country": "United Kingdom"
    },
    {
        "three": "lng-T",
        "name": "Language",
        "transliterable": true,
        "codepage": 65001,
        "country": "United Kingdom"
    }
]
```

### Metadata values

The variables are shown below:

* `lng`: The short name of the language
  * The type of this variable is a **string**
* `name`: The name of the language
  * The type of this variable is a **string**
* `transliterable`: Whether the language is transliterable
  * The type of this variable is a **boolean**
* `codepage`: The codepage to use (Windows only)
  * The type of this variable is an **integer**
* `country`: The country in which the language is being used
  * The type of this variable is a **string**

### Program parameters

Optionally, the parameters can be specified below:

* `-custom`: Generates custom languages only
* `-normal`: Generates normal languages only
* `-all`: Generates all language
* `-singular`: Generates a single language. A language is required if this parameter is passed
* `-dry`: Generates languages, but without saving any changes
* `-resources`: (for internal use only) Copies the generated files to the kernel resources

### Outputs

Once the JSON files are generated in the memory, the program attempts to save them to a path defined in the `Paths.CustomLanguagesPath` variable, which usually resolves to `KSLanguages` under the kernel configuration directory.

For normal languages, they either get saved to `Translations/Output` in the same path as the kernel executable or to the kernel resources folder if `--CopyToResources` is passed to the program.

The output files are in the following format:

```json
{
  "Name": "English (UK)",
  "Transliterable": false,
  "Localizations": [
    "Text here",
    (...)
  ]
}
```
