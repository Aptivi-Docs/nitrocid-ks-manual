---
description: Editing your text is easy!
icon: spell-check
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/editors/text-editor
---

# Text Editor

<figure><img src="../../../.gitbook/assets/image (43) (1).png" alt=""><figcaption></figcaption></figure>

This text editor shell provides you an ability to edit any and all the text files. The `edit` command infers the file type whether it's the text file, the JSON file, or the binary file. It contains many editing tools described in the below section by invoking its commands.

***

## <mark style="color:$primary;">Interactive TUI</mark>

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

In addition to the text editor being a shell, you can switch to an alternative mode when you're in the shell by executing the `tui` command. This way, you'll get access to the fully interactive text editor.

The interactive text editor works like any other interactive text editor, especially the well-known text editing utility available on Unix systems, [vi](https://en.m.wikipedia.org/wiki/Vi) and [vim](https://www.vim.org/). However, it's just that it's different in terms of how it operates.

The currently selected character in the current line is highlighted with the yellow color, depending on your kernel theme.

<details>

<summary>Controls (normal mode)</summary>

Here are some of the common controls:

<table><thead><tr><th width="139.9947509765625">Key</th><th>Action</th></tr></thead><tbody><tr><td><code>ESC</code></td><td>Exits the TUI</td></tr><tr><td><code>K</code></td><td>Gets a list of available keybindings</td></tr><tr><td><code>X</code></td><td>Deletes current character</td></tr><tr><td><code>F1</code></td><td>Inserts a new line after the current line and moves down</td></tr><tr><td><code>F2</code></td><td>Removes a current line and moves up</td></tr><tr><td><code>Shift + F1</code></td><td>Inserts a new line after the current line</td></tr><tr><td><code>Shift + F2</code></td><td>Removes a current line</td></tr><tr><td><code>F3</code></td><td>Replaces the text in the current line with another text</td></tr><tr><td><code>Shift + F3</code></td><td>Replaces the text in all the lines with another text</td></tr><tr><td><code>I</code></td><td>Enters the insertion (enter) mode</td></tr><tr><td><code>Left Arrow</code></td><td>Advances one byte backward</td></tr><tr><td><code>Right Arrow</code></td><td>Advances one byte forward</td></tr><tr><td><code>Up Arrow</code></td><td>Advances one line backward</td></tr><tr><td><code>Down Arrow</code></td><td>Advances one line forward</td></tr><tr><td><code>Page Up</code></td><td>Goes to the previous page</td></tr><tr><td><code>Page Down</code></td><td>Goes to the next page</td></tr><tr><td><code>Home</code></td><td>Goes to the beginning of the text file</td></tr><tr><td><code>End</code></td><td>Goes to the end of the text file</td></tr></tbody></table>

</details>

<details>

<summary>Controls (insert mode)</summary>

When insertion mode is on, you can input any text, erase unnecessary text, and so on. This gives you an ability to edit text interactively. Here are the available controls for you to use:

<table><thead><tr><th width="139.99481201171875">Key</th><th>Action</th></tr></thead><tbody><tr><td><code>Enter</code></td><td>Inserts a new line after the current line and moves down</td></tr><tr><td><code>Esc</code></td><td>Goes back to the viewer mode</td></tr><tr><td><code>Left Arrow</code></td><td>Advances one byte backward</td></tr><tr><td><code>Right Arrow</code></td><td>Advances one byte forward</td></tr><tr><td><code>Up Arrow</code></td><td>Advances one line backward</td></tr><tr><td><code>Down Arrow</code></td><td>Advances one line forward</td></tr><tr><td><code>Page Up</code></td><td>Goes to the previous page</td></tr><tr><td><code>Page Down</code></td><td>Goes to the next page</td></tr><tr><td><code>Home</code></td><td>Goes to the beginning of the text file</td></tr><tr><td><code>End</code></td><td>Goes to the end of the text file</td></tr></tbody></table>

</details>
