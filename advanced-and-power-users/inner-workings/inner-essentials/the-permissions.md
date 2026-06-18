---
description: How do the permissions work?
icon: key
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/the-permissions
---

# The Permissions

Permissions are the authorities that are permitted to the user. It allows the kernel user to gain slightly more power than the absolute normal user.

***

## <mark style="color:$primary;">How do permissions get read?</mark>

When the kernel starts up, it reads the `permissions` array in the configuration for each user. If it finds a permission in the array, it calls the `PermissionsTools.GrantPermission()` function under the `Nitrocid.Security.Permissions` namespace.

{% hint style="info" %}
The call to the above function requires the `ManagePermissions` permission to be granted in the current user.
{% endhint %}

***

## <mark style="color:$primary;">Granting and revoking permissions</mark>

This function gets all the permissions that may have been fused together by the call to this function (adding multiple permissions at once) and checks them one by one to see if it's granted. If not yet granted, it adds the permission to the granted permissions list. It then saves the changes to the configuration file.

In the case of a user being part of a group that is granted several permissions, a user is automatically granted permissions from that group. This is called inheritance, since it's basically an inheritance of permissions from a group to all the users that are members of that group.

The function that does the reverse operation of granting permissions (revoking the permission) is `RevokePermission()`.

***

## <mark style="color:$primary;">Requesting permissions</mark>

If you want your mod to request additional permissions, we prefer to use the `Demand()` function which handles multiple permissions at once.

You can also manually demand one permission type by issuing the `IsPermissionGranted()` function like this:

```csharp
if (!PermissionsTools.IsPermissionGranted(PermissionTypes.type))
    throw new KernelException(KernelExceptionType.PermissionDenied);
```

***

## <mark style="color:$primary;">Permission types</mark>

In kernel permissions there are several types that can be fused together with the OR operator with two or more than two enumerations.

<table><thead><tr><th width="230.33331298828125">Permission</th><th width="91.3333740234375">Value</th><th>Description</th></tr></thead><tbody><tr><td><code>ManagePower</code></td><td>1</td><td>Allows the user to manage power</td></tr><tr><td><code>ManagePermissions</code></td><td>2</td><td>Allows the user to manage permissions</td></tr><tr><td><code>RunStrictCommands</code></td><td>4</td><td>Allows the user to run strict commands</td></tr><tr><td><code>ManageFilesystem</code></td><td>8</td><td>Allows the user to perform the filesystem operations</td></tr><tr><td><code>ManipulateSettings</code></td><td>16</td><td>Allows the user to manipulate with the kernel settings</td></tr><tr><td><code>ExecuteScripts</code></td><td>32</td><td>Allows the user to execute UESH scripts</td></tr><tr><td><code>ExecuteProcesses</code></td><td>64</td><td>Allows the user to execute processes</td></tr><tr><td><code>ManageUsers</code></td><td>128</td><td>Allows the user to manage the users</td></tr><tr><td><code>ManageMods</code></td><td>256</td><td>Allows the user to manage the kernel mods</td></tr><tr><td><code>ManageGroups</code></td><td>512</td><td>Allows the user to manage the user groups</td></tr><tr><td><code>IntermodCommunication</code></td><td>1024</td><td>Allows the user to run mod commands that depend on inter-mod communication</td></tr><tr><td><code>OpenAdminShell</code></td><td>2048</td><td>Allows the user to open an administrative shell</td></tr><tr><td><code>OpenDebugShell</code></td><td>4096</td><td>Allows the user to open a debug shell</td></tr><tr><td><code>InteraddonCommunication</code></td><td>8192</td><td>Allows the user to run commands that depend on inter-addon communication</td></tr><tr><td><code>UseSudo</code></td><td>16384</td><td>Allows the user to use the sudo command</td></tr></tbody></table>
