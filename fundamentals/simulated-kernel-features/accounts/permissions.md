---
description: Did you have permission to do this?
icon: unlock
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/accounts/permissions
---

# Permissions

Permissions indicate what actions that your user or any of the other users are allowed or denied. They can be used to allow or deny users access to some features in the real-world systems. For example, in the filesystem permissions found in Linux systems, if your user isn't granted the execute permission for a specific file, trying to execute said file will give you the permission denied message, preventing the execution of this file.

***

## <mark style="color:$primary;">Permissions in Nitrocid</mark>

In the simulated system, it only simulates the permission types that can be granted or denied to the users. These can be used to control the users what administrative actions they can do and what they can't. There is a permission editing facility that you can use by invoking the `perm` command.

You can do two things: allow and deny. However, if the target user is the administrator (their `admin` flag being set to `true`), all of the permissions, even unlisted, will be granted.

### <mark style="color:$primary;">Examples</mark>

For example, consider the following cases:

<details>

<summary>Case 1: Permission management not granted</summary>

The below screenshot shows that the first normal user, `johnSanders`, can't manipulate the permissions because they don't have the permission management granted.

<figure><img src="../../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Case 2: Permission management granted</summary>

The below screenshot also shows the second non-administrative user, `john.d`, being granted the permission manipulation authority, so they can use the `perm` command to edit permissions for any user.

<figure><img src="../../../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

</details>

### <mark style="color:$primary;">Usage</mark>

To use this utility, choose what you want to do with the target user's permissions and follow the steps below. You can consult the permissions list under the `Advanced and Power Users` category by clicking on the below link.

{% content-ref url="../../../advanced-and-power-users/inner-workings/inner-essentials/the-permissions.md" %}
[the-permissions.md](../../../advanced-and-power-users/inner-workings/inner-essentials/the-permissions.md)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Operations</mark>

There are common operations that you can do to manage the permissions.

<details>

<summary>Grant permissions</summary>

<figure><img src="../../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

You're looking to grant a user permissions. Follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the permission management authority
2. Execute the `perm` command to grant the permission
   * The full usage of the `perm allow` command is `perm <userName> <allow> <perm>`
3. Log out of the user and log-in to the new user

</details>

<details>

<summary>Revoke permissions</summary>

<figure><img src="../../../.gitbook/assets/image (40) (1).png" alt=""><figcaption></figcaption></figure>

If you no longer want a user to be granted a specific permission, follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the permission management authority
2. Execute the `perm` command to revoke the permission
   * The full usage of the `perm revoke` command is `perm <userName> <revoke> <perm>`
3. Log out of the user and log-in to the new user

</details>

<details>

<summary>Grant a permission to a group</summary>

<figure><img src="../../../.gitbook/assets/image (41) (1).png" alt=""><figcaption></figcaption></figure>

You're looking to grant a user permissions. Follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the permission management authority
2. Execute the `permgroup` command to grant the permission
   * The full usage of the `permgroup allow` command is `permgroup <groupName> <allow> <perm>`
3. Log out of the user and log-in to a user that is part of a group

</details>

<details>

<summary>Revoke a permission from a group</summary>

<figure><img src="../../../.gitbook/assets/image (42) (1).png" alt=""><figcaption></figcaption></figure>

If you no longer want a group to be granted a specific permission, follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the permission management authority
2. Execute the `permgroup` command to revoke the permission
   * The full usage of the `permgroup revoke` command is `permgroup <groupName> <revoke> <perm>`
3. Log out of the user and log-in to a user that is part of a group

</details>

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the permission management permission granted to be able to use the manipulation commands.
{% endhint %}
