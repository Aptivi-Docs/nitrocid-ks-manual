---
description: How do the permissions work?
---

# 🔐 The Permissions

Permissions are the authorities that are permitted to the user. It allows the kernel user to gain slightly more power than the absolute normal user.

When the kernel starts up, it reads the `permissions` array in the configuration for each user. If it finds a permission in the array, it calls the `PermissionsTools.GrantPermission()` function under the `KS.Users.Permissions` namespace.

{% hint style="info" %}
The call to the above function requires the `ManagePermissions` permission to be granted in the current user.
{% endhint %}

This function gets all the permissions that may have been fused together by the call to this function (adding multiple permissions at once) and checks them one by one to see if it's granted. If not yet granted, it adds the permission to the granted permissions list. It then saves the changes to the configuration file.

The function that does the reverse operation of granting permissions (revoking the permission) is `RevokePermission()`.

{% hint style="info" %}
If you want your mod to request additional permissions, we prefer to use the `Demand()` function which handles multiple permissions at once.
{% endhint %}

You can also manually demand one permission type by issuing the `IsPermissionGranted()` function like this:

```csharp
if (!PermissionsTools.IsPermissionGranted(PermissionTypes.type))
    throw new KernelException(KernelExceptionType.PermissionDenied);
```

...where the `type` is one of the following types:

* `ManagePower`: Allows the user to manage power
  * Flag value is 1
* `ManagePermissions`: Allows the user to manage permissions
  * Flag value is 2
* `RunStrictCommands`: Allows the user to run strict commands
  * Flag value is 4
