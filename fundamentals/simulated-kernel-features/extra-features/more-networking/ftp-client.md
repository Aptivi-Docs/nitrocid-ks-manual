---
description: How to use your FTP client
icon: folder-open
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/more-networking/ftp-client
---

# FTP Client

<figure><img src="../../../../.gitbook/assets/image (192) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
As of 0.1.0, this feature has been moved to the kernel addons.
{% endhint %}

File Transfer Protocol (FTP) was a standard network protocol used to transfer files from computer to another computer in the network. It used the client-server architecture to manage data and control connections between the source and the target. It normally uses the plain text usernames and passwords to authenticate to the FTP server, but if the server was configured for guest authentication, the client could log in to the server without the username and the password. It first appeared on April 16, 1971.

Various computer applications for both the connection to the FTP server and the hosting service for the protocol have appeared for multiple platforms, like Windows and Linux. The simulated kernel contains the FTP shell which allows you to perform FTP operations on a remote server.

{% hint style="warning" %}
The FTP protocol in general is being replaced by SFTP, although it's kept for historical purposes. This client should be used as a last resort.
{% endhint %}

***

## <mark style="color:$primary;">How to connect</mark>

To connect the client to the FTP server, you have two ways to initiate a connection to the server, which is connecting directly from the main shell, and connecting inside the FTP shell.

<details>

<summary>Connecting to FTP from UESH</summary>

To connect directly from UESH, please follow the steps:

1. Use the `ftp <server>` command
2. Authenticate using your username and your password
3. Select an FTP profile
4. You're connected!

</details>

<details>

<summary>Connecting to FTP inside the FTP shell</summary>

To connect to your FTP server inside the FTP shell, please follow the steps:

1. Use the `ftp` command
2. Now, execute the `connect <server>` command
3. Authenticate using your username and your password
4. Select an FTP profile
5. You're connected!

</details>

***

## <mark style="color:$primary;">Interactive TUI</mark>

To learn more about the local interactive TUI that you can use within the FTP shell, consult this page:

{% content-ref url="../../files-and-folders/" %}
[files-and-folders](../../files-and-folders/)
{% endcontent-ref %}
