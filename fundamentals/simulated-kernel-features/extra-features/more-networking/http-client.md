---
description: Make your HTTP requests
icon: globe
---

# HTTP Client

<figure><img src="../../../../.gitbook/assets/image (51) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
As of 0.1.0, this feature has been moved to the kernel addons.
{% endhint %}

Hypertext Transfer Protocol (HTTP) is an application layer protocol in the Internet protocol suite model for distributed, collaborative, and hypermedia information systems. HTTP is the foundation of data communication for the World Wide Web, where hypertext documents include hyperlinks to other resources that the user can easily access, for example by a mouse click or by tapping the screen in a web browser.

The simulated kernel attempts to provide the request functionalities for the entire HTTP protocol by giving you the HTTP client, which is just a shell with HTTP request commands.

## Connecting to an HTTP server

To be able to use the below commands that are listed in the below section, you have to be connected to an HTTP server by following the below instructions:

1. Open the HTTP shell by invoking the `http` command
2. Use the `setsite` command to point to the target host that hosts the HTTP server
   * Usage: `setsite <host>`
3. Now, execute any of the below request commands to interact with the server

{% hint style="danger" %}
You can ignore certificate errors by setting the `IgnoreCertificateErrors` property in the kernel settings to true, but we don't recommend that you do that, especially when it comes to untrustworthy servers, as the server you're trying to connect to might be compromised.
{% endhint %}

## Commands

To get access to the list of commands, consult the below page:

{% content-ref url="../../shells/addon-commands-list.md" %}
[addon-commands-list.md](../../shells/addon-commands-list.md)
{% endcontent-ref %}
