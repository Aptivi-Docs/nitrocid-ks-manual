---
description: How to upgrade Nitrocid KS on macOS
icon: apple
---

# macOS

The only way to upgrade your kernel in macOS is to unpack the updated kernel files manually. This method also works for bleeding-edge builds, though you have to use unzip instead. To upgrade, follow these steps:

1. Download the latest release ZIP file from [this page](https://github.com/Aptivi/Kernel-Simulator/releases).
2. Unpack the ZIP archive to any folder of your choice
3. Open your favorite terminal emulator, like iTerm2, and change the working directory to a folder containing the Nitrocid KS executable
4. Execute `dotnet Nitrocid.dll` to start the kernel
