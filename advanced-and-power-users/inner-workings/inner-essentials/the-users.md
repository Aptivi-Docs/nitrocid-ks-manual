---
description: This page describes the internal workings of the username management
icon: users
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/the-users
---

# The Users

Nitrocid KS provides you with a rich user management that does basic and advanced operations, such as creating a user, removing a user, listing users, and so on.

***

## <mark style="color:$primary;">User locking</mark>

You can lock the modification of a user by using the following functions:

{% code title="UserManagement.cs" lineNumbers="true" %}
```csharp
public static void LockUser(string User) { }
public static void UnlockUser(string User) { }
public static bool IsLocked(string User) { }
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

***

## <mark style="color:$primary;">Login handlers</mark>

<figure><img src="../../../.gitbook/assets/image (187) (1).png" alt=""><figcaption></figcaption></figure>

Login handlers are login interfaces in which Nitrocid summons in order to commence a login process, just after all the necessary components of the kernel have finished loading.

<details>

<summary>Login flows</summary>

They provide three login flows:

<table><thead><tr><th width="220.6666259765625">Flow</th><th>Description</th></tr></thead><tbody><tr><td><code>LoginScreen()</code></td><td>This is the first step for every login handler to stylize their login screen. It can be simple (textual) or modern (interactive). The return value determines whether to proceed to the user selector screen or to refresh itself (useful for shutdown/reboot options).</td></tr><tr><td><code>UserSelector()</code></td><td>This is the second stage in which the login handler must prompt for the username and return the correct username that exists. Additionally, you can make it return the username that the user input.</td></tr><tr><td><code>PasswordHandler(user)</code></td><td>This is the final stage in which the handler should ask the password for any selected user. For security reasons, we've chosen not to allow auto-logins for passwordless users, except the modern logon handler provided by Nitrocid.</td></tr></tbody></table>

Login handlers don't handle the 2FA authentication for a user that has the second factor enabled, for security reasons. The login manager handles it so that users are always greeted with the 2FA code screen.

{% hint style="danger" %}
Be honest when dealing with the return values for both `UserSelector` and `PasswordHandler`. Make sure that you use the correct values for both of them. `PasswordHandler` returns either `true` or `false` in the following conditions:

* `true`: if the password is valid
* `false`: if the password is invalid
{% endhint %}

</details>

<details>

<summary>Registering handlers</summary>

You can now add or remove your custom login handlers to make your kernel use your login screen. To add your handler, you can use the `RegisterHandler()` function to add it to the list of available handlers. This allows you to customize your login screen to the one that you made.

```csharp
public static void RegisterHandler(string name, BaseLoginHandler handler) { }
```

After that, you should be able to find your login handler when trying to change your login screen using the `settings` command.

{% hint style="info" %}
If you want your mod to automatically populate your custom login handler on startup, you may use the `RegisterHandler()` function, but make sure to unregister it using the `UnregisterHandler()` function when your mod is being unloaded.
{% endhint %}

</details>

<details>

<summary>Unregistering handlers</summary>

Similarly, if you want to unregister your login handler, you can do so by using the `UnregisterHandler()` function.

```csharp
public static void UnregisterHandler(string name) { }
```

</details>
