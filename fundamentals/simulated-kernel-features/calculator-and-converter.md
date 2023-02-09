---
description: Calculate your mathematical expressions and convert units
---

# ⚖ Calculator and Converter

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

The calculator is used to perform arithmetic operations, ranging from the simplest operations to the most complex ones, powered by the StringMath library. Its syntax reference can be reviewed in the below link to the official library documentation.

{% embed url="https://github.com/miroiu/string-math/blob/master/README.md" %}

<figure><img src="../../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

The unit converter, however, is used to easily convert the source units to different units, like centimeters to meters. It's powered by the UnitsNet library. You can consult the list of units UnitsNet supports here:

{% embed url="https://github.com/angularsen/UnitsNet/tree/master/UnitsNet/GeneratedCode/Units" %}

To use both the programs, refer to the command usages and individual explanations below.

* `calc <expression>`
  * Calculates the specific arithmetical expression
* `unitconv <unittype> <quantity> <sourceunit> <targetunit>`
  * Converts the unit by quantity and type from the source unit to the target unit

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

You can use the `listunits` command to get all the available units by type.
