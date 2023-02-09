---
description: Networking in general and its children
---

# 🌍 Networking

Networking in general allows your device to connect to other devices in either your local network – that allows you to make a connection to other systems that are found in the same network – and across the Internet – that allows you to connect to all the other systems found world-wide – to actually access resources found on these systems and, across the LAN, save time trying to go back and forth to the target system to pull and push data.

To simulate this functionality, the simulated kernel provides several features, including the basic networking tools like downloading and uploading files to the remote PCs. These functions can be invoked with built-in main commands.

### Download a file

<figure><img src="../../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

To download a file from a computer or an Internet website, use the `get` command to download to your current working directory. Use the following execution method to download a URL: `get <URL>`

{% hint style="warning" %}
Note that this command currently doesn't support downloading a file to other file names in other directories.
{% endhint %}

### Upload a file

To upload a file to either a local computer or to an Internet URL, use the `put` command to do this action. Depending on the URL, you must have administrative privileges on the URL to be able to upload a file. Usage: `put <file> <URL>`.

## What else?

There are much more features related to networking than just uploading and downloading things. In fact, the kernel provides several of the shells which allow you to communicate with the computers using different protocols, like HTTP and SFTP, and use it for getting information, like the RSS client that actually works as a shell.

Select a shell below to get started.

{% content-ref url="ftp-client.md" %}
[ftp-client.md](ftp-client.md)
{% endcontent-ref %}

{% content-ref url="sftp-client.md" %}
[sftp-client.md](sftp-client.md)
{% endcontent-ref %}

{% content-ref url="http-client.md" %}
[http-client.md](http-client.md)
{% endcontent-ref %}

{% content-ref url="rss-client.md" %}
[rss-client.md](rss-client.md)
{% endcontent-ref %}

{% content-ref url="mail-client.md" %}
[mail-client.md](mail-client.md)
{% endcontent-ref %}
