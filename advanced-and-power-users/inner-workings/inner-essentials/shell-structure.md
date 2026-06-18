---
description: Explaining the inner workings of all the kernel shells
icon: square-terminal
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

## Return codes

The kernel exceptions can be used as return codes, though you'll have to reference to a class, called `KernelExceptionTools`, to be able to get an error code by exception type using the `GetErrorCode()` function. In addition to that, you can also use it with an instance of a kernel exception instance, in case you've wrapped the code with the try...catch clause and that you're catching all the `KernelException` errors, which almost all APIs throw on either a failure condition or an invalid operation.

{% hint style="info" %}
All kernel exception codes consist of `10000` added with the enumeration number of the kernel exception type.
{% endhint %}

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

## Error codes

The error code variable, `MESHErrorCode`, holds information about the last process error code, whether it's a success (a zero value) or a failure (non-zero value). In addition to what Terminaux already provides, these values are supported:

### Error codes that come from the commands

* `10000 + KernelExceptionType`
  * Some commands throw this value from any `KernelException` that is thrown by the command executor. Indicates that the command failed to perform its operation, but the kernel already knows about it.
    * Example: If `KernelExceptionType.Config` is thrown from the command executor, and the command knows how to return this exception as an error code, such as using `KernelExceptionTools.GetErrorCode()`, then it'll return the sum of `10000 + 7`, which is `10007`.

### Command-specific error codes

* `1`
  * Indicates that the command answered n to the confirmation (FTP and SFTP's `del` command)
* `2`
  * Indicates that either the real or the imaginary number is not valid (`imaginary` command)
* `3`
  * Indicates that the unit type is not found (`unitconv` command)
* `4`
  * Indicates that the hashes don't match (`verify` command)
* `5`
  * Indicates that the version code can't be formed (`version` command)
  * Indicates that the action taken is invalid (`todo` command)
* `6`
  * Indicates that the version code can't be formed (`platform` command)
* `7`
  * Indicates that the line endings converter can't convert binary files (`convertlineendings` command)
* `8`
  * Indicates that the note number is not numeric (`removenote` command)
* `9`
  * Indicates that the repository has been modified (`checkout` command)
* `10`
  * Indicates that the branch doesn't exist (`checkout` command)
* `11`
  * Indicates that the repository has been modified (`fetch` command)
* `12`
  * Indicates that the remote doesn't exist (`fetch` command)
* `13`
  * Indicates that there are no remotes to pull updates from (`fetch` command)
* `14`
  * Indicates that you need to identify yourself (`pull` command)
* `15`
  * Indicates that you need to identify yourself (`maketag` and `commit` command)
* `16`
  * Indicates that the culture is not found (`altdate` command)
* `17`
  * Indicates that there is no such lyric file (`playlyric` command)
* `18`
  * Indicates that the number of times is invalid (`repeat` command)
* `19`
  * Indicates that repeat can't repeat itself (`repeat` command)
* `20`
  * Indicates that the number of columns is invalid (`wraptext` command)
* `21`
  * Indicates that the extension handler is not registered (`getdefaultexthandler` command)
* `22`
  * Indicates that the extension handler is not registered (`getexthandlers` command)
* `23`
  * Indicates that the extension is not registered (`setexthandler` command)
* `24`
  * Indicates that the extension implementer is not registered (`setexthandler` command)
* `25`
  * Indicates that the port number is invalid (`netfminfo` command)
* `26`
  * Indicates that the number of seconds or the drink name is invalid (`caffeine` command)
* `27`
  * Indicates that there is no such lyric file (`lyriclines` command)
* `28`
  * Indicates that there is no config or key (`getconfigvalue`, `setconfigvalue`, and `lsconfigvalues` command)
* `29`
  * Indicates that the music file is not found (`playsound` command)
* `30`
  * Indicates that the MPG123 library has timed out (`playsound` command)
  * Indicates that the music file is not specified (`musicplayer` command)
* `31`
  * Indicates that the music file is not found (`musicplayer` command)
* `32`
  * Indicates that there are no caffeine alerts to abort (`caffeine` command)
* `33`
  * Indicates that this command is not supported on Windows (`showmainbuffer` command)
* `34`
  * Indicates that the dock is not found (`dock` command)
