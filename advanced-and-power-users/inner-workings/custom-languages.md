---
description: How to define your custom languages.
---

# 🌐 Custom Languages

When you extract the binary folder of Nitrocid KS, you may see a folder called `CustomLanguages`. Inside it, you can see the `Metadata.json` file that holds language metadata as described in the previous article. Before reading this, you must understand the multilingual kernel feature and how it works by clicking on the below link.

{% content-ref url="multilingual-kernel-flow.md" %}
[multilingual-kernel-flow.md](multilingual-kernel-flow.md)
{% endcontent-ref %}

Customized languages play an important role in being a building block for making your custom localization. This feature contains two separate folders:

* `<KSExecutablePath>/CustomLanguages`
  * This is the folder which you should place the source `.txt` files containing all your string translations. You should implement all the translations found in the `eng.txt` file, usually shipped with the Nitrocid KS binary.
* `<KSConfigPath>/KSLanguages`
  * This is the folder that hosts all your custom language JSON files containing the translation metadata and the necessary translation data.

When the kernel starts up, it attempts to install all the custom languages found in the `KSLanguages` path to the language store found within the language manager. This way, the kernel configuration reader will understand that your custom language exists.

## Build your language

Cool! So, you want to build your language? First, open the `Metadata.json`︎ file found in the `CustomLanguages` folder. Write details about your language in their appropriate places. For quick reference, here's an excerpt from the metadata JSON prototype:

```json
}
    "lng": {
        "name": "My Language",
        "transliterable": false,
        "codepage": 932
    }
}
```

Again, the codepage parameter is optional. If you want your language to be able to be transliterated, make two metadata information about your target language, but append the `-T` postfix to one of the metadata information name, for example:

```json
}
    "lng": {
        "name": "My Language",
        "transliterable": true
    },
    "lng-T": {
        "name": "My Language",
        "transliterable": true,
        "codepage": 932
    }
}
```

After you filled in the metadata information about languages you want to create, make a text file with the name of the short language name (`lng` and not `My Language`) for each language with the `.txt` extension, like this: `lng.txt`

Now, head to `Translations/eng.txt` and use it as a reference to translate all the strings found there to your target language. Put all your translations to the newly-created file.

{% hint style="danger" %}
Both `eng.txt` and your language text file **MUST** have the exact same line numbers!
{% endhint %}

After this is done, launch KSJsonifyLocales either by double-clicking the executable file (usually `KSJsonifyLocales.exe`) or by opening the terminal to the executable path and executing the `dotnet KSJsonifyLocales.dll` command.

{% hint style="info" %}
You can also let this program generate only the custom locale information by passing the `--CustomOnly` argument to it.
{% endhint %}

## Test your language

After `KSJsonifyLocales` finishes compiling the JSON file containing your translation, you should be able to find the resulting file in the `<KSConfigPath>/KSLanguages` folder.

Open Nitrocid KS, and change your system language or your user language to your customized language.

### Changing your kernel language

If you want your language to be used in the entire kernel, follow these steps:

1. Log in to any user account _that has administrative permissions or access to the kernel settings program_
2. Execute the `settings` command
3. Go to `General` section
4. Go to `Language` entry
5. Select your language. Your language should be there among the list of the kernel languages.

### Changing your user language

If you want your language to be used just for your user account, follow these steps:

1. Make sure that Nitrocid KS is shut down. If you skip this step, restart Nitrocid KS after you finish following this instruction.
2. In your host system, navigate to the kernel configuration path (`%LOCALAPPDATA%/KS/` or `~/.config/ks/`)
3. Open your favorite text editor to `Users.json`
4. Create the `preferredlanguage` key if it doesn't exist, then change its value to your three-letter language name.
5. Save the file, and start Nitrocid KS
6. Log-in to your target account. The language should change to your custom language.

## Other options for the generator

This locale generator comes with options to change how it works. These switches provide the following functions: (Switches with the `(INT)` suffix are reserved for internal usage only)

* `--CustomOnly`
  * Restricts the generator to custom languages
* `--NormalOnly` `(INT)`
  * Restricts the generator to normal languages
* `--All` `(INT)`
  * Generates all the languages (default)
* `--Singular <lang>`
  * Restricts the generator to a single custom or normal language
* `--CopyToResources` `(INT)`
  * Copies the resulting normal language outputs to the resources folder

## Installing custom languages by hand

If you have a custom language file and you want to quickly install it without having to restart the entire kernel, you can use the `langman` command to use the following parameters:

* `load <lang>`
  * Loads the custom language.
* `unload <lang>`
  * Unloads the custom language.
* `reload <lang>`
  * Reloads the custom language. Synonymous to the sequence of the `unload` and the `reload` parameters.

To check that your language is installed, use `list <lang>` to verify that your language is there and that its information is available.

{% hint style="info" %}
For mods that want to install or uninstall custom languages, you can use the API functions found within the `LanguageManager` module.
{% endhint %}
