---
description: What are accounts in the kernel?
---

# 👤 Accounts

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Operating systems usually provide the user account functionality to allow more than one person to use the same computer. Each person has their own accounts on their computers to store their personal information and data, including their user profiles and their contents.

The concept of accounts in the kernel is to provide the same functionality, but the simulator only simulates the user accounts, not their home paths. Like all the operating systems, the simulator can manage all the user accounts.

## Manipulation

The operations can be performed on the users to manage them. Scroll down to the section you want.

### Add user accounts

In the real-world, if there is a new person willing to use your computer to store their personal documents and information, you can add such user to the computer. This can be done by going to your system's settings to add the user.

<figure><img src="../../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

The same thing can be simulated in Nitrocid KS. To add a new user account, follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the user management permission
2. Execute the `adduser` command to make a new user. The username is needed to be able to create your new user.
   * The full usage of the `adduser` command is `adduser <user> [pass] [confirmpass]`
3. Log out of the user and log-in to the new user

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the user management permission granted to be able to use this command.
{% endhint %}

### Change your password

In case you need to change your password to something more secure, or you need to add your password, you'll go to the user account section of the system settings to add or change your password.

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

In the simulated kernel, there is a command dedicated to changing the user password. You can use this command to perform this operation.

1. Log-in to the system account, root, or any of the administrators or users that has at least the user management permission
2. Execute the `chpwd` command to change the password. If you want to add the password to a user, leave the `UserPass` argument blank
   * The full usage of the `chpwd` command is `chpwd <Username> <UserPass> <newPass> <confirm>`
3. Log out of the user and log-in to the new user with the new password

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the user management permission granted to be able to use this command.
{% endhint %}

### Rename your user

If you want to rename your own user, or if you accidentally made a typo in someone else's username and you want to change it to the right name, you can use the user management portion of the operating system to rename the affected user.

<figure><img src="../../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

The simulated kernel simulates this functionality using the `chusrname` command. To use it, follow these steps:

1. Log-in to the system account, root, or any of the administrators or users that has at least the user management permission
2. Execute the `chusrname` command to change the username
   * The full usage of the `chusrname` command is `chusrname <oldUserName> <newUserName>`
3. Log out of the user and log-in to the new user

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the user management permission granted to be able to use this command.
{% endhint %}

### Remove a user

If the person or a user no longer wants to use your computer, or if they're migrating their data from your computer to their brand-new PC, you can remove their user and all their data associated with it.

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

The simulated kernel simulates the user removal function. Follow these steps to remove a user from the kernel:

1. Log-in to the system account, root, or any of the administrators or users that has at least the user management permission
2. Execute the `rmuser` command to remove the user
   * The full usage of the `rmuser` command is `rmuser <Username>`
3. Log out of the user and log-in to the new user with the new password

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the user management permission granted to be able to use this command.
{% endhint %}

### List existing users

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

If you want to get a list of available usernames that the kernel recognized, you can no longer have to log out of your account to see the list. In the real-world systems, you can get a list of accounts by going to the users section of the system settings. Follow these steps to get the list:

1. Log-in to any available account
2. Execute the `lsusers` command

## Permissions

All users have specific permissions. To get more information about this feature, click on the link below.

{% content-ref url="permissions.md" %}
[permissions.md](permissions.md)
{% endcontent-ref %}
