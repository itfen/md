---
layout: post
title:  "重置终端提示符"
categories:
comments: true
share: true
---

因为 rvm 版本原因，终端（Terminal）的命令 `$ 符号前指示设备名的字符变成了
 125，之前也变过，不知道怎么恢复的了。网上查了一下原来那串个叫 Prompt（提示符）。

通过命令：

```bash
PS1='$(networksetup -getcomputername):\W \u\$ '
```

可以恢复到 Mac 默认的提示符，（来源: [How to return terminal prompt to default? \| Apple Support Communities](https://discussions.apple.com/thread/3617486)）

具体每个参数的意义参考（来源: [Learning the bash Shell, 3rd Edition / O'Reilly Press](http://shop.oreilly.com/product/9780596009656.do)）：

Prompting variables

If you have seen enough experienced UNIX users at work, you may already have realized that the shell's prompt is not engraved in stone. Many of these users have all kinds of things encoded in their prompts. It is possible to put useful information into the prompt, including the date and the current directory.

Actually , bash uses four prompt strings. They are stored in the variables PS1, PS2, PS3, and PS4. The first of these is called the primary prompt string; it is your usual shell prompt, and its default value is "\s-\v\$ ". Many people like to set their primary prompt string to something containing their login name. Here is one way to do this:

PS1="\u--> "

The \u tells bash to insert the name of the current user into the prompt string. If your user name is alice, your prompt string will be "alice—>". If you are a C shell user and, like many such people, are used to having a history number in your prompt string, bash can do this similarly to the C shell: if the sequence \! is used in the prompt string, it will substitute the history number. Thus, if you define your prompt string to be:

PS1="\u \!--> "

then your prompts will be like alice 1—>, alice 2—>, and so on.

But perhaps the most useful way to set up your prompt string is so that it always contains your current directory. This way, you needn't type pwd to remember where you are. Here's how:

PS1="\w--> "


Table of prompt customizations that are available :

\a  The ASCII bell character (007)

\A  The current time in 24-hour HH:MM format

\d  The date in "Weekday Month Day" format

\D {format} The format is passed to strftime(3) and the result is inserted into the prompt string; an empty format results in a locale-specific time representation; the braces are required

\e  The ASCII escape character (033)

\H  The hostname

\h  The hostname up to the first "."

\j  The number of jobs currently managed by the shell

\l  The basename of the shell's terminal device name

\n  A carriage return and line feed

\r  A carriage return

\s  The name of the shell

\T  The current time in 12-hour HH:MM:SS format

\t  The current time in HH:MM:SS format

\@  The current time in 12-hour a.m./p.m. format

\u  The username of the current user

\v  The version of bash (e.g., 2.00)

\V  The release of bash; the version and patchlevel (e.g., 2.00.0)

\w  The current working directory

\W  The basename of the current working directory

\#  The command number of the current command

\!  The history number of the current command

\$  If the effective UID is 0, print a #, otherwise print a $

\nnn    Character code in octal

\\  Print a backslash

\[  Begin a sequence of non-printing characters, such as terminal control sequences

\]  End a sequence of non-printing characters

PS2 is called the secondary prompt string; its default value is >. It is used when you type an incomplete line and hit RETURN, as an indication that you must finish your command.
