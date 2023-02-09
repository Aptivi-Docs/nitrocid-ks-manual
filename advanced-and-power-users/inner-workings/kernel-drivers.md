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

Each driver contains its own interface containing its own method definitions and their signatures. These interfaces are the ones that you must implement with your mod. The most basic interface for the kernel drivers is `IDriver` found in the same namespace, which is implemented by the driver-specific interfaces.

The final driver class implementation must implement both the base driver-specific base class and its interface, such as:

```csharp
internal class Terminal : BaseConsoleDriver, IConsoleDriver
```

If you have a kernel driver that you wish to register, you'll have to register the kernel driver, passing it the `IDriver` interface for your driver and the appropriate type. You can use the `DriverHandler.RegisterDriver()` function to perform this operation, but you should set the current driver to your driver for the target wrappers, like the methods found in the `KS.Files` namespace that call the current filesystem driver, using the `SetDriver<T>()` function.

{% hint style="danger" %}
Be sure to unregister your driver with the `UnregisterDriver()` function, or your driver will not get updated in the list of kernel drivers!
{% endhint %}
