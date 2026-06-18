---
description: Group of users are here
icon: people-group
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/accounts/groups
---

# Groups

Grouping the users is a common task for user management, because the groups not only organize users in a consistent manner, but they also derive permissions and other rules to all the users that are part in a group. For example, if a group has a permission that would allow users inside a group to use administrative commands, all the users will get that permission.

To derive the permissions to some of the users that you've added to a group, you'll have to grant a permission to the group permissions. This is explained in depth in the Permissions page, which you can consult below:

{% content-ref url="permissions.md" %}
[permissions.md](permissions.md)
{% endcontent-ref %}

***

## <mark style="color:$primary;">Operations</mark>

There are common operations that you can do to manage the groups and their permissions.

<details>

<summary>Adding groups</summary>

<figure><img src="../../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

To add a group to the list of available groups, you can use the `addgroup` command. You need to specify a group name that will organize the user accounts based on the role and what is this group for.

</details>

<details>

<summary>Removing groups</summary>

<figure><img src="../../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

You can remove a group from the list of available groups if you no longer want a specific group using the `rmgroup` command. You need to specify a group name that exists to be able to remove it.

</details>

<details>

<summary>Adding users to a group</summary>

<figure><img src="../../../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

You can add a user to an existing group to organize a user by using the `addusertogroup` command so that the user gets permissions from the group. You need to specify an existing user and an existing group that the user didn't join to be able to add a user to the group.

</details>

<details>

<summary>Removing users from a group</summary>

<figure><img src="../../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

You can remove an unwanted user from an existing group using the `rmuserfromgroup` command so that the target user is no longer a member of that target group. You need to specify an existing user and an existing group that the user joined to be able to remove a user from the group.

</details>

{% hint style="warning" %}
Note that your account must have either the administrative permissions enabled or the group management permission granted to be able to use the manipulation commands.
{% endhint %}
