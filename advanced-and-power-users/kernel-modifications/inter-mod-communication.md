---
description: Two or more than two mods talking to each other in Nitrocid
---

# 📞 Inter-Mod Communication

Inter-Mod Communication allows your mods to execute the publicly-available functions of another mod. It allows you to connect two or more than two mods with each other in a mechanism that doesn't interfere with the other mod's operations.

{% hint style="warning" %}
Currently, this feature only supports communications by function delegates, but we'll add support for more communication methods to make mod connection easier.
{% endhint %}

### How to make a function publicly accessible?

You can make a function publicly accessible in one mod by implementing the `PubliclyAvailableFunctions` with a read-only dictionary that contains all your publicly-available functions in your main mod entry point.

{% code title="Interface declaration" %}
```csharp
ReadOnlyDictionary<string, Delegate> PubliclyAvailableFunctions { get; }
```
{% endcode %}

The key is the function name that the mod manager uses to search for a function when invoking the function executor. The value, which is a delegate of either a function or a method (subs in Visual Basic), can either take no parameters or take parameters of varying sizes.

To execute custom mod functions in another mod, you must specify the mod name and the function to execute in the `ExecuteCustomModFunction()` method:

```csharp
public static object ExecuteCustomModFunction(string modName, string functionName)
public static object ExecuteCustomModFunction(string modName, string functionName, params object[] parameters)
```

{% hint style="info" %}
You must specify the main mod name in the above function, since it uses that name to fetch all mod parts and query them for available functions.

`ExecuteCustomModFunction()` returns `null` under the following conditions:

* There are no functions in all the mod parts from your mod.
* There is no function that goes by the name of the specified function name that you plan to execute.
* There is a function, but the delegate is unspecified.
{% endhint %}
