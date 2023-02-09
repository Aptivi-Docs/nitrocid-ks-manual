---
description: Debugging the kernel on LAN
---

# 🛰 Remote Debugging

Remote debugging allows you to remotely diagnose the kernel live. It uses TCP networking to listen to the configurable port.

If remote debugging is enabled on your kernel configuration, it starts the remote debugger under the following configuration (for those who use the firewall):

* Socket: TCP
* Port: `3014` (configurable)
* Transfer: Inbound and Outbound

## Connecting

Once the remote debugger starts, you can connect to it using the raw TCP connection to the server. To initiate the connection, select a platform:

### Windows

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

You can establish a connection to the remote debugger using [PuTTY](https://putty.org/) or an equivalent software. Once you install this, fill the below forms to make a connection:

* Host Name (or IP address): Host of the remote debugger
* Port: `3014` (configurable)
* Type: `Raw`

Click on Connect and you should be able to see debugging messages from the remote host.

### Linux

You can use the `nc` (netcat) command to connect to a remote debugger using a raw connection. Execute the command in this form: `nc <host> <port>`︎, where:

* `<host>`: Host of the remote debugger
* `<port>`: `3014` (configurable)

You should be able to see debugging messages once the connection to the remote debugger has been established.

## Remote debug chat

The chatting feature was added to the remote debugger to allow chatting with the other users debugging the same kernel to discuss what is happening in the kernel.

Every device connected to the remote debugger using the provided connection information will have their entries added to the remote debug device configuration file. They'll be told to register their device with a name before they can chat.

Pressing ENTER will post a message to the kernel debugger, causing everyone who connected to the debugger to see the message live.
