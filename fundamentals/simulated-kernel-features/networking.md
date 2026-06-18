---
description: Networking in general and its shells
icon: globe-wifi
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/networking
---

# Networking

Networking in general allows your device to connect to other devices in either your local network – that allows you to make a connection to other systems that are found in the same network – and across the Internet – that allows you to connect to all the other systems found world-wide – to actually access resources found on these systems and, across the LAN, save time trying to go back and forth to the target system to pull and push data.

***

## <mark style="color:$primary;">Networking in Nitrocid</mark>

To simulate this functionality, the simulated kernel provides several features, including the basic networking tools like downloading and uploading files to the remote PCs. These functions can be invoked with built-in main commands.

<details>

<summary>Download a file</summary>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

To download a file, small or large, from a computer or an Internet website, use the `get` command to download to your current working directory.

Use the following execution method to download: `get [-output=path] <URL>`

</details>

<details>

<summary>Upload a file</summary>

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

To upload a file to either a local computer or to an Internet URL, use the `put` command to do this action. Depending on the URL, you must have administrative privileges on the URL to be able to upload a file.

Use the following execution method to upload: `put <file> <URL>`.

</details>

***

## <mark style="color:$primary;">What else?</mark>

There are much more features related to networking than just uploading and downloading things. In fact, the kernel provides several of the shells which allow you to communicate with the computers using different protocols, like HTTP and SFTP, and use it for getting information, like the RSS client that actually works as a shell.

However, they are only available as kernel addons, so consult the below page:

{% content-ref url="extra-features/more-networking/" %}
[more-networking](extra-features/more-networking/)
{% endcontent-ref %}
