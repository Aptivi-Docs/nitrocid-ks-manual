---
description: How the kernel drivers work and their role in the kernel
---

# 🔌 Kernel Drivers

The kernel drivers allows your kernel to provide interfaces for different purposes, from console to filesystem. This is to present the kernel your implementation of different driver types. It's not a device driver, though!

The kernel drivers can be called using either the properties that point to the current driver of each driver type or the `DriverHandler.GetDriver<TResult>()` function found under the `KS.Drivers` namespace. These two will return an appropriate driver interface that actually allows you to call their functions that each driver of the same type implements. The types of kernel drivers are listed below:

| Driver     | Interface           | Base                   | Description                     |
| ---------- | ------------------- | ---------------------- | ------------------------------- |
| Random     | `IRandomDriver`     | `BaseRandomDriver`     | Random number generator drivers |
| Console    | `IConsoleDriver`    | `BaseConsoleDriver`    | Console drivers                 |
| Network    | `INetworkDriver`    | `BaseNetworkDriver`    | Network drivers                 |
| Filesystem | `IFilesystemDriver` | `BaseFilesystemDriver` | Filesystem drivers              |
| Encryption | `IEncryptionDriver` | `BaseEncryptionDriver` | Encryption drivers              |
| Regexp     | `IRegexpDriver`     | `BaseRegexpDriver`     | Regular expression drivers      |

### Mods and Drivers

{% hint style="warning" %}
Your kernel modifications **should** reference local versions of driver properties, like `CurrentConsoleDriverLocal`, unless it's not possible.
{% endhint %}

Each driver contains its own interface containing its own method definitions and their signatures. These interfaces are the ones that you must implement with your mod. The most basic interface for the kernel drivers is `IDriver` found in the same namespace, which is implemented by the driver-specific interfaces.

The final driver class implementation must implement both the base driver-specific base class and its interface, such as:

```csharp
internal class Terminal : BaseConsoleDriver, IConsoleDriver
```

If you have a kernel driver that you wish to register, you'll have to register the kernel driver, passing it the `IDriver` interface for your driver and the appropriate type. You can use the `DriverHandler.RegisterDriver()` function to perform this operation, but you should set the current driver to your driver for the target wrappers, like the methods found in the `KS.Files` namespace that call the current filesystem driver, using the `SetDriverSafe<T>()` function.

{% hint style="warning" %}
The `SetDriver<T>()` function can be used, but doesn't prevent you from using internal drivers. We advice you to use the `SetDriverSafe<T>()` function instead.
{% endhint %}

{% hint style="danger" %}
Be sure to unregister your driver with the `UnregisterDriver()` function, or your driver will not get updated in the list of kernel drivers!
{% endhint %}

### Local drivers

If you want to temporarily to use a driver without affecting the entire kernel and its configuration, you can use this feature to temporarily switch drivers of supported types.

Assuming that your mod uses local drivers to do their actions, like `CurrentConsoleDriverLocal`, you must use the following functions **in order**:

* `BeginLocalDriverSafe<T>()`: This notifies the kernel that the mod is going to use the provided driver temporarily.
* `EndLocalDriver<T>()`: This notifies the kernel that the mod is done with the temporary driver.

Where `T` is the interface type of the driver found in the above table at the start of this page.

{% hint style="warning" %}
The `BeginLocalDriver<T>()` function can be used, but doesn't prevent you from using internal drivers. We advice you to use the `BeginLocalDriverSafe<T>()` function instead.
{% endhint %}

{% hint style="danger" %}
Be sure to execute the two above functions in the order specified above. Forgetting to call `EndLocalDriver<T>()` after you're done with the driver can cause the kernel to think that the mod is going to use your local driver forever.
{% endhint %}

### Driver Configuration

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

The `settings` application now lets you set your system-wide kernel drivers up in a completely new section called `Kernel driver settings`. It lets you configure current drivers for each supported driver type.

In order to configure your driver, select one of the driver types from the settings section shown above by pressing `ENTER`, and select your driver.

{% hint style="info" %}
Like all other settings, you must save your kernel settings to apply your changes across reboots.
{% endhint %}
