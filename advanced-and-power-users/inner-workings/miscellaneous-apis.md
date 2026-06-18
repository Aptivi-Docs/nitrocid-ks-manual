---
description: >-
  Other inner workings that don't fit with the inner essentials and might be
  useful for your mods
icon: galaxy
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/miscellaneous-apis
---

# Miscellaneous APIs

In addition to the essential APIs that are provided with the Nitrocid kernel that allow you to make awesome mods ranging from simple ones to the most complicated ones, Nitrocid provides some of the useful APIs that don't fit with the category but can be helpful when developing mods.

***

## <mark style="color:$primary;">List of misc APIs</mark>

The following APIs can be used in your mods:

<details>

<summary>Kernel version information</summary>

You can get the kernel version information using the following properties from the `KernelReleaseInfo` class:

| Property         | Description                                                                                                 |
| ---------------- | ----------------------------------------------------------------------------------------------------------- |
| `Version`        | Gets the kernel version without the build specifiers.                                                       |
| `VersionFull`    | Gets the kernel version with the build specifiers (essentially the same as the GitHub tag for the release). |
| `VersionFullStr` | Gets the string of `VersionFull`.                                                                           |
| `ApiVersion`     | Gets the kernel API version.                                                                                |

</details>
