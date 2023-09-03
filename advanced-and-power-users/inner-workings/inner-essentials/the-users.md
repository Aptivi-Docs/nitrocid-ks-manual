---
description: This page describes the internal workings of the username management
---

# 👥 The Users

Nitrocid KS provides you with a rich user management that does basic and advanced operations, such as creating a user, removing a user, listing users, and so on.

### User locking

You can lock the modification of a user by using the following functions:

{% code title="UserManagement.cs" lineNumbers="true" %}
```csharp
public static void LockUser(string User)
public static void UnlockUser(string User)
public static bool IsLocked(string User)
```
{% endcode %}

When a user is locked, the following functions can't be run on that user to protect it. This is used by the `sudo` command to protect users running `sudo` from removing the root user or the current user.

* `InitializeUser()`
* `RemoveUser()`
* `ChangeUsername()`
* `ChangePassword()`

{% hint style="warning" %}
Trying to run any of the four functions above results in a `KernelException` if they're executed against a locked user.
{% endhint %}
