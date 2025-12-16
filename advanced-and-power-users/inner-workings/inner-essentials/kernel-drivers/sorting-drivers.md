---
description: Changing how the sorting algorithms work
icon: plug-circle-bolt
---

# Sorting Drivers

The sorting driver is one of the supported driver types on Nitrocid KS. These drivers allow you to change how the sorting works, thus earning dynamic sorting improvements, such as providing fast and efficient array sorting code.

The sorting drivers have the following characteristics:

* Interface: `ISortingDriver`
* Base class: `BaseSortingDriver`

The sorting drivers have the functions that you can optionally override, and are listed in the relevant API documentation.

The `SortingDriverTools` class contains tools to get all the sorting drivers and their names and set a sorting driver as a default. The driver management tools also allow you to do the same thing, though you'll have to specify the driver type.
