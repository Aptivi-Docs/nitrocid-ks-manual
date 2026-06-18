---
description: Transfer your files securely between your servers and your PC
icon: lock-keyhole
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/more-networking/sftp-client
---

# SFTP Client

<figure><img src="../../../../.gitbook/assets/image (48) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
As of 0.1.0, this feature has been moved to the kernel addons.
{% endhint %}

This protocol is a modern file transfer protocol that is implemented as part of the Secure SHell (SSH) protocol version 2.0 engineered by the Internet Engineering Task Force (IETF). It allows secure file transfers from the client to the server and from the server to the client.

***

## <mark style="color:$primary;">How to connect</mark>

To connect the client to the SFTP server, you have two ways to initiate a connection to the server, which is connecting directly from the main shell, and connecting inside the SFTP shell.

<details>

<summary>Connecting to SFTP from UESH</summary>

To connect directly from UESH, please follow the steps:

1. Use the `sftp <server>` command
2. Authenticate using your username and your password or your private key
3. You're connected!

</details>

<details>

<summary>Connecting to SFTP inside the SFTP shell</summary>

To connect to your SFTP server inside the SFTP shell, please follow the steps:

1. Use the `sftp` command
2. Now, execute the `connect <server>` command
3. Authenticate using your username and your password or your private key file
4. You're connected!

</details>

***

## <mark style="color:$primary;">Interactive TUI</mark>

To learn more about the local interactive TUI that you can use within the FTP shell, consult this page:

{% content-ref url="../../files-and-folders/" %}
[files-and-folders](../../files-and-folders/)
{% endcontent-ref %}
