---
description: Editing your text is easy!
---

# 📝 Text Editor

<figure><img src="../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

This text editor shell provides you an ability to edit any and all the text files. The `edit` command infers the file type whether it's the text file, the JSON file, or the binary file. It contains many editing tools described in the below section by invoking these commands.

## Commands

These below commands can be used to interact with the text file:

* `addline <text>`
  * Adds a new line with the specified text at the end of the text file
* `addlines`
  * Adds new lines at the end of the text file
* `clear`
  * Deletes the contents of the text file
* `delcharnum <charnumber> <linenumber>`
  * Deletes a character using the column number from the specified line number
* `delline <linenumber> [linenumber2]`
  * Deletes a specified line number or the range of line numbers
* `delword "<word/phrase>" <linenumber> [linenumber2]`
  * Deletes a specified word or phrase in a line number or the range of line numbers
* `editline <linenumber>`
  * Edits a line using a specified line number
* `exitnosave`
  * Exits the text editor without saving any changes
* `print [linenumber] [linenumber2]`
  * Print either the entire text file, a line number, or lines from the first line number to the second one
* `querychar <char> <linenumber/all> [linenumber2]`
  * Queries a character in either the entire text file, a line number, or lines from the first line number to the second one
* `queryword "<word/phrase>" <linenumber/all> [linenumber2]`
  * Queries a word in either the entire text file, a line number, or lines from the first line number to the second one
* `querywordregex "<regex>" <linenumber/all> [linenumber2]`
  * Queries a word using the regular expressions in either the entire text file, a line number, or lines from the first line number to the second one
* `replace "<word/phrase>" "<word/phrase>"`
  * Replaces a word or a phrase in the entire text file with another word or phrase
* `replaceinline "<word/phrase>" "<word/phrase>" <linenumber> [linenumber2]`
  * Replaces a word or a phrase with another word or phrase in a line or lines from the first line number to the second one
* `replaceregex "<regex>" "<word/phrase>"`
  * Replaces a word or a phrase in the entire text file with another word or phrase using regular expressions
* `replaceinlineregex "<regex>" "<word/phrase>" <linenumber> [linenumber2]`
  * Replaces a word or a phrase with another word or phrase in a line or lines from the first line number to the second one using regular expressions
* `save`
  * Saves the changes to the file
