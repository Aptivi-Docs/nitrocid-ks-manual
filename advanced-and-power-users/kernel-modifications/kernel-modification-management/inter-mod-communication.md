---
description: Two or more than two mods talking to each other in Nitrocid
icon: phone
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/kernel-modifications/kernel-modification-management/inter-mod-communication
---

# Inter-Mod Communication

Inter-Mod Communication allows your mods to execute the publicly-available functions of another mod. It allows you to connect two or more than two mods with each other in a mechanism that doesn't interfere with the other mod's operations.

***

## <mark style="color:$primary;">Prerequisites for inter-mod communication</mark>

In order to be able to communicate with the other mods in your mod, you'll need to get the mod types and to select a type that you'll need to work on. This is to avoid ambiguity that may be caused by calling functions, properties, or fields that may have the same name.

***

## <mark style="color:$primary;">Communication tools</mark>

You can do the following to get the type:

<details>

<summary>Listing types</summary>

You can now list all the available public types from a mod. You must use this before being able to perform the rest of the communication functions, such as getting functions and executing them.

{% code title="InterModTools.cs" lineNumbers="true" %}
```csharp
public static Type[] ListAvailableTypes(string modName) { }
```
{% endcode %}

{% hint style="info" %}
In order for a type to appear, it must be public and visible.

The above functions return an empty array under the following conditions:

* There are no public and/or visible types.
{% endhint %}

</details>

<details>

<summary>Getting types</summary>

You can get a specific type from a mod using the fully-qualified type name. These functions are used implicitly when passing the type name instead of the type instance returned by the below functions:

{% code title="InterModTools.cs" lineNumbers="true" %}
```csharp
public static Type GetTypeFromMod(string modName, string typeName) { }
```
{% endcode %}

{% hint style="info" %}
In order for a type to appear, it must be public and visible.

The above functions throw an exception under the following conditions:

* There are no public and/or visible types under the specified type name.
{% endhint %}

</details>

After getting the type, you can now use the communication tools.

<details>

<summary>Calling a publicly accessible mod function</summary>

To execute custom mod functions (which must be public and static) in your mod, you must specify the full mod name, the type that you're working on, and the function to execute in the `ExecuteCustomModFunction()` method:

```csharp
public static object? ExecuteCustomModFunction(string modName, string functionName, string typeName) { }
public static object? ExecuteCustomModFunction(string modName, string functionName, string typeName, params object?[]? parameters) { }
public static object? ExecuteCustomModFunction(string modName, string functionName, Type type) { }
public static object? ExecuteCustomModFunction(string modName, string functionName, Type type, params object?[]? parameters) { }
```

{% hint style="info" %}
You must specify the main mod name in the above function, since it uses that name to query an addon for available functions.

`ExecuteCustomModFunction()` returns `null` under the following conditions:

* There are no functions in all the mods.
* There is a function, but the delegate is unspecified.

It throws an exception if these conditions are true:

* There is no function that goes by the name of the specified function name that you plan to execute.
{% endhint %}

</details>

<details>

<summary>Getting/Setting a value from/to a property or a field</summary>

To get a property value or a field value (which must be public and static) from a mod, you can call the following functions:

```csharp
public static object? GetCustomModPropertyValue(string modName, string propertyName, string typeName) { }
public static object? GetCustomModFieldValue(string modName, string fieldName, string typeName) { }
public static object? GetCustomModPropertyValue(string modName, string propertyName, Type type) { }
public static object? GetCustomModFieldValue(string modName, string fieldName, Type type) { }
```

Similarly, to set a property value or a field value (which must be public and static) declared publicly by an addon, you can call the following functions:

```csharp
public static void SetCustomModPropertyValue(string modName, string propertyName, string typeName, object? value) { }
public static void SetCustomModFieldValue(string modName, string fieldName, string typeName, object? value) { }
public static void SetCustomModPropertyValue(string modName, string propertyName, Type type, object? value) { }
public static void SetCustomModFieldValue(string modName, string fieldName, Type type, object? value) { }
```

{% hint style="info" %}
You must specify the main mod name in the above function, since it uses that name to query an addon for available properties or fields.

`GetCustomModPropertyValue()` and `GetCustomModFieldValue()` return `null` under the following conditions:

* There are no properties or fields in all the mods.
* There is a property or field, but the delegate is unspecified.
* There is a property or field, but they return `null`.

It throws an exception if these conditions are true:

* There is no property or field that goes by the name of the specified name that you plan to execute.
{% endhint %}

</details>

<details>

<summary>Listing functions, properties, and fields</summary>

You can now list all the available functions, properties, and fields from a specific addon using one of the following functions:

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
// For functions
public static Dictionary<string, MethodInfo> ListAvailableFunctions(string modName, string typeName) { }
public static Dictionary<string, MethodInfo> ListAvailableFunctions(string modName, Type type) { }

// For properties
public static Dictionary<string, PropertyInfo> ListAvailableProperties(string modName, string typeName) { }
public static Dictionary<string, PropertyInfo> ListAvailableProperties(string modName, Type type) { }

// For fields
public static Dictionary<string, FieldInfo> ListAvailableFields(string modName, string typeName) { }
public static Dictionary<string, FieldInfo> ListAvailableFields(string modName, Type type) { }
```
{% endcode %}

{% hint style="info" %}
You must specify the main mod name in the above functions and the type that this mod exposes.

The above functions return an empty array under the following conditions:

* There are no accessible public static functions, properties, or fields.
{% endhint %}

</details>

<details>

<summary>Listing function and set property parameters</summary>

You can list all the function and set property parameters in depth by using the following functions:

{% code title="InterAddonTools.cs" lineNumbers="true" %}
```csharp
// Normal functions
public static ParameterInfo[]? GetFunctionParameters(string modName, string functionName, string typeName) { }
public static ParameterInfo[]? GetFunctionParameters(string modName, string functionName, Type type) { }

// Property setters
public static ParameterInfo[]? GetSetPropertyParameters(string modName, string propertyName, string typeName) { }
public static ParameterInfo[]? GetSetPropertyParameters(string modName, string propertyName, Type type) { }
```
{% endcode %}

{% hint style="info" %}
You must specify the main mod name in the above function, since it uses that name to query an addon for available properties or fields.

These functions return `null` under the following conditions:

* There are no properties or functions in all the mods.
* There is a property, but there is no setter.

It throws an exception if these conditions are true:

* There is no property or function that goes by the name of the specified name that you plan to execute.
{% endhint %}

</details>
