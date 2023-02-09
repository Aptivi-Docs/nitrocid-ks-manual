---
description: How to use your FTP client
---

# 🗃 FTP Client

File Transfer Protocol (FTP) was a standard network protocol used to transfer files from computer to another computer in the network. It used the client-server architecture to manage data and control connections between the source and the target. It normally uses the plain text usernames and passwords to authenticate to the FTP server, but if the server was configured for guest authentication, the client could log in to the server without the username and the password. It first appeared on April 16, 1971.

Various computer applications for both the connection to the FTP server and the hosting service for the protocol have appeared for multiple platforms, like Windows and Linux. The simulated kernel contains the FTP shell which allows you to perform FTP operations on a remote server.

{% hint style="warning" %}
The FTP protocol in general is being replaced by SFTP, although it's kept for historical purposes. This client should be used as a last resort.
{% endhint %}

## How to connect

To connect the client to the FTP server, you have two ways to initiate a connection to the server, which is connecting directly from the main shell, and connecting inside the FTP shell.

### Connecting to FTP from UESH

To connect directly from UESH, please follow the steps:

1. Use the `ftp <server>` command
2. Authenticate using your username and your password
3. Select an FTP profile
4. You're connected!

### Connecting to FTP inside the FTP shell

To connect to your FTP server inside the FTP shell, please follow the steps:

1. Use the `ftp` command
2. Now, execute the `connect <server>` command
3. Authenticate using your username and your password
4. Select an FTP profile
5. You're connected!

## Commands

These below commands are used to perform operations on your FTP server, but the commands found in the bottom of the list are administrative commands. Such commands need an authenticated account with the permissions for performing the operations committed by these commands.

### Normal commands

* `cdl <directory>`
  * Changes the local working directory. The folder should exist in your computer.
* `cdr <directory>`
  * Changes the remote working directory. The folder should exist in your FTP server.
* `disconnect [-f]`
  * Disconnects your client from your FTP server
* `execute <command>`
  * Executes your custom FTP server query
* `get <file> [output]`
  * Download a remote file from your FTP server to the local directory
* `getfolder <folder> [outputfolder]`
  * Downloads a remote folder and its contents from your FTP server to the local directory
* `info`
  * Gets information about the FTP server
* `lsl [-showdetails|-suppressmessages] [dir]`
  * Lists the directory contents from either your current working local directory or a specified local folder
* `lsr [-showdetails] [dir]`
  * Lists the directory contents from either your current working remote directory or a specified remote folder
* `pwdl`
  * Gets the current working local directory
* `pwdr`
  * Gets the current working remote directory
* `quickconnect`
  * Opens the connection selection to connect to your FTP server quickly
* `sumfile <file> <MD5/SHA1/SHA256/SHA512/CRC>`
  * Gets the hash sum of a remote file. Please note that it only works for FTP servers that support the hash sum calculation
* `sumfiles <folder> <MD5/SHA1/SHA256/SHA512/CRC>`
  * Gets the hash sum of the remote files. Please note that it only works for FTP servers that support the hash sum calculation
* `type <a/b>`
  * Sets the entire session type. `a` stands for ASCII (text) file transfer, while `b` stands for binary transfer. The default type is the binary transfer.

### Administrative commands

* `cp <sourcefileordir> <targetfileordir>`
  * Copies the remote file or directory to the target file or directory.
* `del <file>`
  * Deletes a file from the remote server
* `mv <sourcefileordir> <targetfileordir>`
  * Moves the source remote file or directory to the target file or directory
* `put <file> [output]`
  * Uploads the entire local file to the FTP server in the current working remote directory
* `putfolder <folder> [outputfolder]`
  * Uploads the entire local folder to the FTP server in the current working remote directory
* `perm <file> <permnumber>`
  * Sets the remote file UNIX permissions on FTP servers that run UNIX or its derivatives
