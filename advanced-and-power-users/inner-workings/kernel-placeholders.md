---
description: Do you want to <placeholder>?
---

# 🪧 Kernel Placeholders

Kernel placeholders are text variables for any piece of text that are replaced by different elements found within the kernel. They are parsed in several different areas of the kernel, the most famous example being the MOTD and the MAL messages.

The probing takes place in the `PlaceParse.ProbePlaces()` function found within the `KS.Misc.Probers.Placeholder` namespace. The following types of text use this function to parse the placeholders:

* MOTD and MAL messages
* Username prompt and their derivatives for each shell
* Password prompt and their derivatives for each shell
* Mail progress style
* Mail progress style (single)
* `echo` command
* Manual page information style
* GPG prompt style
* Custom welcome banner
* Remote debugger message format
* RSS feed URL prompt style
* Manual page contents
* Download and upload progress for network transfers
* Progress Clock screensaver's informational text variables

These are the placeholders and what possible values are going to replace them when being parsed:

| Placeholder                       | Value                                                                              |
| --------------------------------- | ---------------------------------------------------------------------------------- |
| `<user>`                          | Current logged-in username                                                         |
| `<ftpuser>`                       | Current logged-in FTP username                                                     |
| `<ftpaddr>`                       | Current logged-in FTP server address                                               |
| `<currentftpdirectory>`           | Current FTP remote directory                                                       |
| `<currentftplocaldirectory>`      | Current FTP local directory                                                        |
| `<currentftplocaldirectoryname>`  | Current FTP local directory name                                                   |
| `<sftpuser>`                      | Current logged-in SFTP username                                                    |
| `<sftpaddr>`                      | Current logged-in SFTP server address                                              |
| `<currentsftpdirectory>`          | Current SFTP remote directory                                                      |
| `<currentsftplocaldirectory>`     | Current SFTP local directory                                                       |
| `<currentsftplocaldirectoryname>` | Current SFTP local directory name                                                  |
| `<mailuser>`                      | Current logged-in mail address                                                     |
| `<mailaddr>`                      | Current logged-in mail server                                                      |
| `<currentmaildirectory>`          | Current mail directory                                                             |
| `<host>`                          | Host name of the kernel                                                            |
| `<currentdirectory>`              | Current directory                                                                  |
| `<currentdirectoryname>`          | Current directory name                                                             |
| `<shortdate>`                     | Short date                                                                         |
| `<longdate>`                      | Long date                                                                          |
| `<shorttime>`                     | Short time                                                                         |
| `<longtime>`                      | Long time                                                                          |
| `<date>`                          | Today's date                                                                       |
| `<time>`                          | The time right now                                                                 |
| `<timezone>`                      | Local timezone                                                                     |
| `<summertimezone>`                | Summer local timezone                                                              |
| `<system>`                        | Operating system                                                                   |
| `<newline>`                       | New line                                                                           |
| `<dollar>`                        | User administrative indicator                                                      |
| `<randomfile>`                    | Random file path                                                                   |
| `<randomfolder>`                  | Random directory path                                                              |
| `<f:reset>`                       | Reset the foreground color                                                         |
| `<b:reset>`                       | Reset the background color                                                         |
| `<f:color>`                       | Sets the foreground color (where `color` is either `0-255` or `0-255;0-255;0-255`) |
| `<b:color>`                       | Sets the background color (where `color` is either `0-255` or `0-255;0-255;0-255`) |
| `<$var>`                          | Uses the value of a UESH variable (where `var` is an initialized variable)         |
