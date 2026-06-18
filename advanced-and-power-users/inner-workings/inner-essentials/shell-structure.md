---
description: Explaining the inner workings of all the kernel shells
icon: square-terminal
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/advanced-and-power-users/inner-workings/inner-essentials/shell-structure
---

# Shell Structure

Kernel shells can be built by implementing two different interfaces and base classes. Why two? Because the shell handler relies on:

* `BaseShell` and `IShell`: To hold shell type and initialization code
* `BaseShellInfo<ShellType>` and `IShellInfo`: To hold shell commands and the base shell

To learn more about general information about shells, consult the page below:

{% content-ref url="https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/shells" %}
[Shells](https://app.gitbook.com/s/G0KrE9Uk2AiblqjWtpAo/usage/input-reader/shells)
{% endcontent-ref %}

If you want to know about Nitrocid-specific additions, read on.

***

## <mark style="color:$primary;">Networked shells</mark>

Networked shells are shells that are aware of the network client object, such as the FTP client or the SFT client object. They are useful for building CLI applications that use built-in shells to interact with a remote server over the network.

<details>

<summary>Attaching and Detaching</summary>

Every single client that Nitrocid implements support attachment to existing connections and detachment from the current connection. When you use one of the clients for the first time, it lets you create a new connection. From there, you have to specify some info about which server you're going to connect, the username, and the password, depending on the client.

When you're connected to any server, you can detach the current connection, which causes you to go back to your shell when you're still connected. In order to attach back to your session, use the same command that you used to create a new connection to connect to the existing server or to create a second new connection.

To detach, simply use the `detach` command to go back to your shell.

</details>

<details>

<summary>Speed dial for networked shells</summary>

Speed dial allows you to quickly connect to servers with your username, your address, your port, and your custom network configuration. This will save time in having to enter address information manually each time you connect to the same server.

When you invoke a command that launches your networked shell (FTP for example), a selection window shows up with the option to either select an established connection, an option to create a new connection manually, or connect to the saved networks using the speed dial functionality.

</details>

***

## <mark style="color:$primary;">Return codes</mark>

The kernel exceptions can be used as return codes, though you'll have to reference to a class, called `KernelExceptionTools`, to be able to get an error code by exception type using the `GetErrorCode()` function.

In addition to that, you can also use it with an instance of a kernel exception instance, in case you've wrapped the code with the `try` and `catch` clause and that you're catching all the `KernelException` errors, which almost all APIs throw on either a failure condition or an invalid operation.

{% hint style="info" %}
All kernel exception codes consist of `10000` added with the enumeration number of the kernel exception type.
{% endhint %}

<details>

<summary>Example of getting error code from kernel exception type</summary>

Here's a minimal example of what exit does when you're trying to exit the mother shell:

<pre class="language-csharp"><code class="lang-csharp">public override int Execute(CommandParameters parameters, ref string variableValue)
{
    if (ShellManager.IsOnMotherShell())
    {
        TextWriters.Write(Translate.DoTranslation("You can't exit the mother shell. Did you mean to log out of your account, shut the kernel down, or reboot it?"), KernelColorType.Error);
<strong>        return KernelExceptionTools.GetErrorCode(KernelExceptionType.ShellOperation);
</strong>    }
    ShellManager.KillShell();
    return 0;
}
</code></pre>

</details>

<details>

<summary>Error code list</summary>

The error code variable, `MESHErrorCode`, holds information about the last process error code, whether it's a success (a zero value) or a failure (non-zero value).

In addition to what Terminaux already provides, these values are supported:

#### <mark style="color:$primary;">Error codes that come from the commands</mark>

<table><thead><tr><th width="260.3333740234375">Error code</th><th>Description</th></tr></thead><tbody><tr><td><code>-3</code></td><td>Indicates that the command is attempting to be run in maintenance mode and the command forbids that</td></tr><tr><td><code>-4</code></td><td>Indicates that the command is a strict command and the user doesn't have permissions to execute it</td></tr><tr><td><code>10000 + KernelExceptionType</code></td><td>Some commands throw this value from any <code>KernelException</code> that is thrown by the command executor. Indicates that the command failed to perform its operation, but the kernel already knows about it.<br><br>Example: If <code>KernelExceptionType.Config</code> is thrown from the command executor, and the command knows how to return this exception as an error code, such as using <code>KernelExceptionTools.GetErrorCode()</code>, then it'll return the sum of <code>10000 + 7</code>, which is <code>10007</code>.</td></tr></tbody></table>

#### <mark style="color:$primary;">Command-specific error codes</mark>

<table><thead><tr><th width="129.666748046875">Error code</th><th>Description</th></tr></thead><tbody><tr><td><code>1</code></td><td>Indicates that the command answered n to the confirmation (FTP and SFTP's <code>del</code> command)</td></tr><tr><td><code>2</code></td><td>Indicates that either the real or the imaginary number is not valid (<code>imaginary</code> command)</td></tr><tr><td><code>3</code></td><td>Indicates that the unit type is not found (<code>listunits</code> command)</td></tr><tr><td></td><td>Theme preview has exited by user request (<code>themeprev</code> command)</td></tr><tr><td></td><td>Theme set has exited by user request (<code>themeset</code> command)</td></tr><tr><td><code>4</code></td><td>Indicates that the hashes don't match (<code>verify</code> command)</td></tr><tr><td><code>5</code></td><td>Indicates that the version code can't be formed (<code>version</code> command)</td></tr><tr><td></td><td>Indicates that the action taken is invalid (<code>todo</code> command)</td></tr><tr><td><code>6</code></td><td>Indicates that the version code can't be formed (<code>platform</code> command)</td></tr><tr><td><code>7</code></td><td>Indicates that the line endings converter can't convert binary files (<code>convertlineendings</code> command)</td></tr><tr><td><code>8</code></td><td>Indicates that the note number is not numeric (<code>removenote</code> command)</td></tr><tr><td><code>9</code></td><td>Indicates that the repository has been modified (<code>checkout</code> command)</td></tr><tr><td><code>10</code></td><td>Indicates that the branch doesn't exist (<code>checkout</code> command)</td></tr><tr><td><code>11</code></td><td>Indicates that the repository has been modified (<code>fetch</code> command)</td></tr><tr><td><code>12</code></td><td>Indicates that the remote doesn't exist (<code>fetch</code> command)</td></tr><tr><td><code>13</code></td><td>Indicates that there are no remotes to pull updates from (<code>fetch</code> command)</td></tr><tr><td><code>14</code></td><td>Indicates that you need to identify yourself (<code>pull</code> command)</td></tr><tr><td><code>15</code></td><td>Indicates that you need to identify yourself (<code>maketag</code> and <code>commit</code> command)</td></tr><tr><td><code>16</code></td><td>Indicates that the culture is not found (<code>altdate</code> command)</td></tr><tr><td><code>17</code></td><td>Indicates that there is no such lyric file (<code>playlyric</code> command)</td></tr><tr><td><code>20</code></td><td>Indicates that the number of columns is invalid (<code>wraptext</code> command)</td></tr><tr><td><code>21</code></td><td>Indicates that the extension handler is not registered (<code>getdefaultexthandler</code> command)</td></tr><tr><td><code>22</code></td><td>Indicates that the extension handler is not registered (<code>getexthandlers</code> command)</td></tr><tr><td><code>23</code></td><td>Indicates that the extension is not registered (<code>setexthandler</code> command)</td></tr><tr><td><code>24</code></td><td>Indicates that the extension implementer is not registered (<code>setexthandler</code> command)</td></tr><tr><td><code>25</code></td><td>Indicates that the port number is invalid (<code>netfminfo</code> command)</td></tr><tr><td><code>26</code></td><td>Indicates that the number of seconds or the drink name is invalid (<code>caffeine</code> command)</td></tr><tr><td><code>27</code></td><td>Indicates that there is no such lyric file (<code>lyriclines</code> command)</td></tr><tr><td><code>28</code></td><td>Indicates that there is no config or key (<code>getconfigvalue</code>, <code>setconfigvalue</code>, and <code>lsconfigvalues</code> command)</td></tr><tr><td><code>29</code></td><td>Indicates that the music file is not found (<code>playsound</code> command)</td></tr><tr><td><code>30</code></td><td>Indicates that the MPG123 library has timed out (<code>playsound</code> command)</td></tr><tr><td><code>32</code></td><td>Indicates that there are no caffeine alerts to abort (<code>caffeine</code> command)</td></tr><tr><td><code>33</code></td><td>Indicates that this command is not supported on Windows (<code>showmainbuffer</code> command)</td></tr><tr><td><code>34</code></td><td>Indicates that the dock is not found (<code>dock</code> command)</td></tr><tr><td><code>35</code></td><td>Indicates that user didn't provide file or content (<code>pastebin</code> command)</td></tr><tr><td><code>36</code></td><td>Indicates that the provider type of pastebin is not raw, http, or https (<code>pastebin</code> command)</td></tr><tr><td><code>37</code></td><td>Indicates that pastebin has failed (<code>pastebin</code> command)</td></tr><tr><td><code>38</code></td><td>Indicates that latitude and longitude is needed (<code>weather</code> command)</td></tr><tr><td><code>39</code></td><td>Indicates that the path is not provided or image is not found (<code>preview</code> command)</td></tr><tr><td><code>40</code></td><td>Indicates that the API call for AlphaVantage has failed (<code>stock</code> command)</td></tr><tr><td><code>41</code></td><td>Indicates that there is no SQL database connection (<code>dbinfo</code> command)</td></tr><tr><td><code>42</code></td><td>Indicates that the file stream is not open for JSON (<code>tui</code> command)</td></tr><tr><td><code>43</code></td><td>Indicates that there is no repository (all Git commands)</td></tr><tr><td><code>44</code></td><td>Indicates that there is no chemical substance (<code>element</code> command)</td></tr><tr><td><code>45</code></td><td>Indicates that the expiry date info is invalid (<code>expiry</code> command)</td></tr><tr><td><code>46</code></td><td>Indicates that the mode is not specified (<code>ismode</code> command)</td></tr></tbody></table>

</details>
