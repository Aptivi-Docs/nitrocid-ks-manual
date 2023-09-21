---
description: This page describes the internal workings of the username management
---

# 👥 The Users

Nitrocid KS provides you with a rich user management that does basic and advanced operations, such as creating a user, removing a user, listing users, and so on.

## User locking

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

## Login handlers

Login handlers are login interfaces in which Nitrocid summons in order to commence a login process, just after all the necessary components of the kernel have finished loading. They provide three login flows:

* `LoginScreen()`
  * This is the first step for every login handler to stylize their login screen. It can be simple (textual) or modern (interactive)
* `UserSelector()`
  * This is the second stage in which the login handler must prompt for the username and return the correct username that exists. Additionally, you can make it return the username that the user input.
* `PasswordHandler(user)`
  * This is the final stage in which the handler should ask the password for any selected user. For security reasons, we've chosen not to allow auto-logins for passwordless users, except the modern logon handler provided by Nitrocid.

{% hint style="danger" %}
Be honest when dealing with the return values for both `UserSelector` and `PasswordHandler`. Make sure that you use the correct values for both of them. `PasswordHandler` returns either `true` or `false` in the follwoing conditions:

* `true`: if the password is valid
* `false`: if the password is invalid
{% endhint %}

{% hint style="warning" %}
Currently, we don't support registering and unregistering your own login handler. Until improvements are made to the login system, we suggest that you don't create one.
{% endhint %}
