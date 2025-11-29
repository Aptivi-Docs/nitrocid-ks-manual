---
description: How remote procedure works
icon: satellite
---

# Remote Procedure

Remote Procedure is a remote controlling system for the kernel that allows external devices connected to the network to execute commands remotely. It can be triggered on and off in the kernel settings. By default, it's turned on.

For those who use the firewall, here's the configuration used for a standard RPC installation:

* Socket: UDP
* Port: `12345` (configurable)
* Transfer: Incoming and Outgoing

Basically, it listens to any commands received from any device. The commands are listed below:

* `<Request:Shutdown>(IP)`: Remotely shuts the system down
* `<Request:Reboot>(IP)`: Remotely reboots the system
* `<Request:RebootSafe>(IP)`: Remotely reboots the system to safe mode
* `<Request:RebootMaintenance>(IP)`: Remotely reboots the system to maintenance mode
* `<Request:RebootDebug>(IP)`: Remotely reboots the system to debug mode
* `<Request:SaveScr>(IP)`: Remotely saves the screen
* `<Request:Exec>(Command)`: Remotely executes the command
* `<Request:Acknowledge>(IP)`: Remotely acknowledges the device
* `<Request:Ping>(IP)`: Remotely acknowledges the device with a notification
* `<Request:Version>(IP)`: Returns the version
* `<Request:VersionCode>(IP)`: Returns the version code
* `<Request:ApiVersion>(IP)`: Returns the API version
* `<Request:ApiVersionCode>(IP)`: Returns the API version code

Some commands support arguments. When the request is made, the kernel translates it to the response as in the following form:

```
TypeConfirm, Args
```

After being translated, the RPC attempts to send the response to the target device. It then translates the confirmation to the appropriate action.

## Nitrocid.Rkm

Nitrocid has a separate application that manages a Nitrocid instance that is running the RPC server without having to run the full Nitrocid executable. When an RPC server is running, the server can be interacted with in the entire network, especially the local area network. Using the port that is configurable, you can send a command to a Nitrocid RPC instance in your network, such as shutting it down and pinging it.

By default, Nitrocid.Rkm runs on the default IP address, which is the loopback interface address `127.0.0.1` (also known as localhost), and the default kernel RPC port mentioned at the beginning of the page. The following switches change how Nitrocid.Rkm connects to the Nitrocid RPC host:

* `--verbose`: Enables verbose logging and extra messages
* `--help`: Lists switches
* `--host`: Specifies the host name or IP address to connect to
* `--port`: Specifies the port number to connect to the host with
* `--command`: A single RPC command that you can pass to the host

When `--command` is not specified, it defaults to the `test` command, which only calls the `<Request:Acknowledge>(IP)` command. This acknowledgement message is always sent, regardless of the command, to verify that we are connected to the correct Nitrocid host. One of the following commands can be specified:

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
