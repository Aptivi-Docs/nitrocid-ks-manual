---
description: Mods talking to an addon or more than one addon in Nitrocid
---

# 📞 Inter-Addon Communication

Inter-Addon Communication allows your mods to execute the publicly-available functions of a kernel addon. It allows your mods to talk to the kernel addons in a mechanism that doesn't interfere with the other end's operations.

{% hint style="info" %}
Currently, there is one addon that utilize this feature, called `Extras - RSS Shell`. It declares only one function to be publicly accessible, which is `GetFirstArticle`.
{% endhint %}

### How to call a publicly accessible addon function?

To execute custom addon functions in your mod, you must specify the full addon name, such as `Extras - RSS Shell`, and the function to execute in the `ExecuteCustomAddonFunction()` method:

```csharp
public static object ExecuteCustomAddonFunction(string addonName, string functionName)
public static object ExecuteCustomAddonFunction(string addonName, string functionName, params object[] parameters)
```

{% hint style="info" %}
You must specify the main addon name in the above function, since it uses that name to query an addon for available functions.

`ExecuteCustomAddonFunction()` returns `null` under the following conditions:

* There are no functions in all the mod parts from your mod.
* There is a function, but the delegate is unspecified.

It throws an exception if these conditions are true:

* There is no function that goes by the name of the specified function name that you plan to execute.
{% endhint %}

### How can I get/set a value from/to a property or a field?

To get a property value or a field value from an addon, you can call the following functions:

```csharp
public static object GetCustomAddonPropertyValue(string addonName, string propertyName)
public static object GetCustomAddonFieldValue(string addonName, string fieldName)
```

Similarly, to set a property value or a field value declared publicly by an addon, you can call the following functions:

```csharp
public static void SetCustomAddonPropertyValue(string addonName, string propertyName, object value)
public static void SetCustomAddonFieldValue(string addonName, string fieldName, object value)
```

{% hint style="info" %}
You must specify the main addon name in the above function, since it uses that name to query an addon for available properties or fields.

`GetCustomModPropertyValue()` and `GetCustomModFieldValue()` return `null` under the following conditions:

* There are no properties or fields in all the mod parts from your mod.
* There is a property or field, but the delegate is unspecified.

It throws an exception if these conditions are true:

* There is no property or field that goes by the name of the specified name that you plan to execute.
{% endhint %}
