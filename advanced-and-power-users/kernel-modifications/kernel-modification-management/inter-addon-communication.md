---
description: Mods talking to an addon or more than one addon in Nitrocid
icon: phone
---

# Inter-Addon Communication

Inter-Addon Communication allows your mods to execute the publicly-available functions of a kernel addon. It allows your mods to talk to the kernel addons in a mechanism that doesn't interfere with the other end's operations.

{% hint style="info" %}
When getting the name of an addon, you can consult the `GetAddonName()` function, indicating what addon you want to use, such as `KnownAddons.ExtrasAmusements` for `Extras - Amusements`.
{% endhint %}

## Prerequisites for inter-addon communication

In order to be able to communicate with the other addons in your mod, you'll need to get the addon types and to select a type that you'll need to work on. This is to avoid ambiguity that may be caused by calling functions, properties, or fields that may have the same name. You can do the following:

### Listing types

You can now list all the available public types from a specific addon. You must use this before being able to perform the rest of the communication functions, such as getting functions and executing them.

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
public static Type[] ListAvailableTypes(KnownAddons addonName)
public static Type[] ListAvailableTypes(string addonName)
```
{% endcode %}

{% hint style="info" %}
In order for a type to appear, it must be public and visible.

The above functions return an empty array under the following conditions:

* There are no public and/or visible types.
{% endhint %}

### Getting types

You can get a specific type from an addon using the fully-qualified type name. These functions are used implicitly when passing the type name instead of the type instance returned by the below functions:

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
public static Type GetTypeFromAddon(KnownAddons addonName, string typeName)
public static Type GetTypeFromAddon(string addonName, string typeName)
```
{% endcode %}

{% hint style="info" %}
In order for a type to appear, it must be public and visible.

The above functions throw an exception under the following conditions:

* There are no public and/or visible types under the specified type name.
{% endhint %}

## Operation

After getting a type, you can call the rest of the inter-addon communication functions.

### How do I call a publicly accessible addon function?

To execute custom addon functions (which must be public and static) in your mod, you must specify the full addon name, such as `Extras - RSS Shell`, the type that you're working on, and the function to execute in the `ExecuteCustomAddonFunction()` method:

```csharp
public static object? ExecuteCustomAddonFunction(KnownAddons addonName, string functionName, string typeName)
public static object? ExecuteCustomAddonFunction(KnownAddons addonName, string functionName, string typeName, params object?[]? parameters)
public static object? ExecuteCustomAddonFunction(string addonName, string functionName, string typeName)
public static object? ExecuteCustomAddonFunction(string addonName, string functionName, string typeName, params object?[]? parameters)
public static object? ExecuteCustomAddonFunction(KnownAddons addonName, string functionName, Type type)
public static object? ExecuteCustomAddonFunction(KnownAddons addonName, string functionName, Type type, params object?[]? parameters)
public static object? ExecuteCustomAddonFunction(string addonName, string functionName, Type type)
public static object? ExecuteCustomAddonFunction(string addonName, string functionName, Type type, params object?[]? parameters)
```

{% hint style="info" %}
You must specify the main addon name in the above function, since it uses that name to query an addon for available functions. Remember, you can use the `KnownAddons` enumeration to simplify things!

`ExecuteCustomAddonFunction()` returns `null` under the following conditions:

* There are no functions in all the addons.
* There is a function, but the delegate is unspecified.

It throws an exception if these conditions are true:

* There is no function that goes by the name of the specified function name that you plan to execute.
{% endhint %}

### How can I get/set a value from/to a property or a field?

To get a property value or a field value (which must be public and static) from an addon, you can call the following functions:

```csharp
public static object? GetCustomAddonPropertyValue(KnownAddons addonName, string propertyName, string typeName)
public static object? GetCustomAddonFieldValue(KnownAddons addonName, string fieldName, string typeName)
public static object? GetCustomAddonPropertyValue(string addonName, string propertyName, string typeName)
public static object? GetCustomAddonFieldValue(string addonName, string fieldName, string typeName)
public static object? GetCustomAddonPropertyValue(KnownAddons addonName, string propertyName, Type type)
public static object? GetCustomAddonFieldValue(KnownAddons addonName, string fieldName, Type type)
public static object? GetCustomAddonPropertyValue(string addonName, string propertyName, Type type)
public static object? GetCustomAddonFieldValue(string addonName, string fieldName, Type type)
```

Similarly, to set a property value or a field value (which must be public and static) declared publicly by an addon, you can call the following functions:

```csharp
public static void SetCustomAddonPropertyValue(KnownAddons addonName, string propertyName, string typeName, object? value)
public static void SetCustomAddonFieldValue(KnownAddons addonName, string fieldName, string typeName, object? value)
public static void SetCustomAddonPropertyValue(string addonName, string propertyName, string typeName, object? value)
public static void SetCustomAddonFieldValue(string addonName, string fieldName, string typeName, object? value)
public static void SetCustomAddonPropertyValue(KnownAddons addonName, string propertyName, Type type, object? value)
public static void SetCustomAddonFieldValue(KnownAddons addonName, string fieldName, Type type, object? value)
public static void SetCustomAddonPropertyValue(string addonName, string propertyName, Type type, object? value)
public static void SetCustomAddonFieldValue(string addonName, string fieldName, Type type, object? value)
```

{% hint style="info" %}
You must specify the main addon name in the above function, since it uses that name to query an addon for available properties or fields. Remember, you can use the `KnownAddons` enumeration to simplify things!

`GetCustomAddonPropertyValue()` and `GetCustomAddonFieldValue()` return `null` under the following conditions:

* There are no properties or fields in all the addons.
* There is a property or field, but the delegate is unspecified.
* There is a property or field, but they return `null`.

It throws an exception if these conditions are true:

* There is no property or field that goes by the name of the specified name that you plan to execute.
{% endhint %}

### Listing functions, properties, and fields

You can now list all the available functions, properties, and fields from a specific addon using one of the following functions:

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
// For functions
public static Dictionary<string, MethodInfo> ListAvailableFunctions(KnownAddons addonName, string typeName)
public static Dictionary<string, MethodInfo> ListAvailableFunctions(KnownAddons addonName, Type type)
public static Dictionary<string, MethodInfo> ListAvailableFunctions(string addonName, string typeName)
public static Dictionary<string, MethodInfo> ListAvailableFunctions(string addonName, Type type)

// For properties
public static Dictionary<string, PropertyInfo> ListAvailableProperties(KnownAddons addonName, string typeName)
public static Dictionary<string, PropertyInfo> ListAvailableProperties(KnownAddons addonName, Type type)
public static Dictionary<string, PropertyInfo> ListAvailableProperties(string addonName, string typeName)
public static Dictionary<string, PropertyInfo> ListAvailableProperties(string addonName, Type type)

// For fields
public static Dictionary<string, FieldInfo> ListAvailableFields(KnownAddons addonName, string typeName)
public static Dictionary<string, FieldInfo> ListAvailableFields(KnownAddons addonName, Type type)
public static Dictionary<string, FieldInfo> ListAvailableFields(string addonName, string typeName)
public static Dictionary<string, FieldInfo> ListAvailableFields(string addonName, Type type)
```
{% endcode %}

{% hint style="info" %}
You must specify the main addon name in the above functions and the type that this addon exposes. Remember, you can use the `KnownAddons` enumeration to simplify things!

The above functions return an empty array under the following conditions:

* There are no accessible public static functions, properties, or fields.
{% endhint %}

### Listing function and set property parameters

You can list all the function and set property parameters in depth by using the following functions:

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
// Normal functions
public static ParameterInfo[]? GetFunctionParameters(KnownAddons addonName, string functionName, string typeName)
public static ParameterInfo[]? GetFunctionParameters(KnownAddons addonName, string functionName, Type type)
public static ParameterInfo[]? GetFunctionParameters(string addonName, string functionName, string typeName)
public static ParameterInfo[]? GetFunctionParameters(string addonName, string functionName, Type type)

// Property setters
public static ParameterInfo[]? GetSetPropertyParameters(KnownAddons addonName, string propertyName, string typeName)
public static ParameterInfo[]? GetSetPropertyParameters(KnownAddons addonName, string propertyName, Type type)
public static ParameterInfo[]? GetSetPropertyParameters(string addonName, string propertyName, string typeName)
public static ParameterInfo[]? GetSetPropertyParameters(string addonName, string propertyName, Type type)
```
{% endcode %}

{% hint style="info" %}
You must specify the main addon name in the above function, since it uses that name to query an addon for available properties or fields. Remember, you can use the `KnownAddons` enumeration to simplify things!

These functions return `null` under the following conditions:

* There are no properties or functions in all the addons.
* There is a property, but there is no setter.

It throws an exception if these conditions are true:

* There is no property or function that goes by the name of the specified name that you plan to execute.
{% endhint %}
