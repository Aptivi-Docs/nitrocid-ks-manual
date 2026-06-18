---
description: How remote procedure works
icon: satellite
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/remote-procedure
---

# Remote Procedure

Remote Procedure is a remote controlling system for the kernel that allows external devices connected to the network to execute commands remotely. It can be triggered on and off in the kernel settings. By default, it's turned on.

For those who use the firewall, here's the configuration used for a standard RPC installation:

* Socket: UDP
* Port: `12345` (configurable)
* Transfer: Incoming and Outgoing

***

## <mark style="color:$primary;">Available commands</mark>

The commands are listed below:

<table><thead><tr><th width="299.333251953125">Command</th><th>Description</th></tr></thead><tbody><tr><td><code>&#x3C;Request:Shutdown>(IP)</code></td><td>Remotely shuts the system down</td></tr><tr><td><code>&#x3C;Request:Reboot>(IP)</code></td><td>Remotely reboots the system</td></tr><tr><td><code>&#x3C;Request:RebootSafe>(IP)</code></td><td>Remotely reboots the system to safe mode</td></tr><tr><td><code>&#x3C;Request:RebootMaintenance>(IP)</code></td><td>Remotely reboots the system to maintenance mode</td></tr><tr><td><code>&#x3C;Request:RebootDebug>(IP)</code></td><td>Remotely reboots the system to debug mode</td></tr><tr><td><code>&#x3C;Request:SaveScr>(IP)</code></td><td>Remotely saves the screen</td></tr><tr><td><code>&#x3C;Request:Exec>(Command)</code></td><td>Remotely executes the command</td></tr><tr><td><code>&#x3C;Request:Acknowledge>(IP)</code></td><td>Remotely acknowledges the device</td></tr><tr><td><code>&#x3C;Request:Ping>(IP)</code></td><td>Remotely acknowledges the device with a notification</td></tr><tr><td><code>&#x3C;Request:Version>(IP)</code></td><td>Returns the version</td></tr><tr><td><code>&#x3C;Request:VersionCode>(IP)</code></td><td>Returns the version code</td></tr><tr><td><code>&#x3C;Request:ApiVersion>(IP)</code></td><td>Returns the API version</td></tr><tr><td><code>&#x3C;Request:ApiVersionCode>(IP)</code></td><td>Returns the API version code</td></tr></tbody></table>

***

## <mark style="color:$primary;">Confirmation</mark>

Some commands support arguments. When the request is made, the kernel translates it to the response as in the following form:

```
TypeConfirm, Args
```

After being translated, the RPC attempts to send the response to the target device. It then translates the confirmation to the appropriate action.

***

## <mark style="color:$primary;">Nitrocid.Rkm</mark>

<figure><img src="../../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Nitrocid has a separate application that manages a Nitrocid instance that is running the RPC server without having to run the full Nitrocid executable. When an RPC server is running, the server can be interacted with in the entire network, especially the local area network. Using the port that is configurable, you can send a command to a Nitrocid RPC instance in your network, such as shutting it down and pinging it.

<details>

<summary>Switches for the app</summary>

The following switches change how Nitrocid.Rkm connects to the Nitrocid RPC host:

<table><thead><tr><th width="120">Switch</th><th>Description</th></tr></thead><tbody><tr><td><code>--verbose</code></td><td>Enables verbose logging and extra messages</td></tr><tr><td><code>--help</code></td><td>Lists switches.</td></tr><tr><td><code>--host</code></td><td>Specifies the host name or IP address to connect to.</td></tr><tr><td><code>--port</code></td><td>Specifies the port number to connect to the host with.</td></tr><tr><td><code>--command</code></td><td>A single RPC command that you can pass to the host.</td></tr></tbody></table>

</details>

<details>

<summary>Defaults for the app</summary>

By default, Nitrocid.Rkm runs on the default IP address, which is the loopback interface address `127.0.0.1` (also known as localhost), and the default kernel RPC port mentioned at the beginning of the page.

When `--command` is not specified, it defaults to the `test` command, which only calls the `<Request:Acknowledge>(IP)` command. This acknowledgement message is always sent, regardless of the command, to verify that we are connected to the correct Nitrocid host.

</details>

<details>

<summary>Available commands</summary>

One of the following commands can be specified:

* `shutdown`
* `reboot`
* `rebootsafe`
* `rebootmaintenance`
* `rebootdebug`
* `savescr`
* `exec`
* `ping`
* `version`
* `versioncode`
* `apiversion`
* `apiversioncode`

</details>
