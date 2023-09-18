---
description: Calculate your mathematical expressions and convert units
---

# ⚖ Unit Converter

{% hint style="info" %}
As of 0.1.0, this feature has been moved to the kernel addons.
{% endhint %}

## CLI version

<figure><img src="../../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

The unit converter is used to easily convert the source units to different units, like centimeters to meters. It's powered by the UnitsNet library. You can consult the list of units UnitsNet supports here:

{% @github-files/github-code-block url="https://github.com/angularsen/UnitsNet/tree/master/UnitsNet/GeneratedCode/Units" %}

To use both the programs, refer to the command usages and individual explanations below.

* `calc <expression>`
  * Calculates the specific arithmetical expression
* `unitconv <unittype> <quantity> <sourceunit> <targetunit>`
  * Converts the unit by quantity and type from the source unit to the target unit

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

You can use the `listunits` command to get all the available units by type.

## TUI version

The TUI version of unit converter allows you to more interactively convert the units. It lets you choose a unit type and a conversion form. Once you're done selecting, you can press F1 to bring up the conversion dialog.

This dialog prompts you for a number (using the source unit) to convert it to the same representation in the target unit. Once you press ENTER, the result will show up.
