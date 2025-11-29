---
description: >-
  Other inner workings that don't fit with the inner essentials and might be
  useful for your mods
icon: galaxy
---

# Miscellaneous APIs

In addition to the essential APIs that are provided with the Nitrocid kernel that allow you to make awesome mods ranging from simple ones to the most complicated ones, Nitrocid provides some of the useful APIs that don't fit with the category but can be helpful when developing mods.

The following APIs can be used in your mods:

## Kernel version information

You can get the kernel version information using the following properties from the `KernelReleaseInfo` class:

* `Version`: Gets the kernel version without the build specifiers
* `VersionFull`: Gets the kernel version with the build specifiers (essentially the same as the GitHub tag for the release)
* `VersionFullStr`: Gets the string of `VersionFull`
* `ApiVersion`: Gets the kernel API version.
