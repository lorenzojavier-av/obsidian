## Objective

Install ZSH with Oh My ZSH and learn the basic features.

## Distributions

ZSH is available in the repositories of nearly every distribution.

## Requirements

A working Linux install with root privileges.

## Difficulty

Easy

## Conventions

-   **#** – requires given [linux commands](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/linux-commands) to be executed with root privileges either directly as a root user or by use of `sudo` command
-   **$** – requires given [linux commands](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/linux-commands) to be executed as a regular non-privileged user

## Introduction

Bash isn’t bad. It gets the job done just fine, but have you ever considered what it’d be like if Bash had some extra features to make it more convenient to work with? That’s more-or-less what ZSH is.

It includes all of the features that you’d expect from Bash, but it also has some really nice additions to make your life easier. Actually, you’ll be amazed at how much easier they make working in the command line.

## Install ZSH

First, you’re going to need to install ZSH. It’s incredibly popular, so you’ll have no problem finding it in your distribution’s repositories.

**Ubuntu/Debian**

$ sudo apt install zsh

**Fedora**

\# dnf -y install zsh

**CentOS**

\# yum -y install zsh

**OpenSUSE**

\# zypper in zsh

**Arch Linux**

\# pacman -S zsh

**Gentoo**

\# emerge --ask zsh

You probably get the idea. It’s possible to use ZSH by just typing it as a command in Bash. That particular terminal will switch to ZSH temporarily. It’s best to just switch permanently, though. It won’t cost you anything, and you can do everything you would normally do the exact same way. Plus, you can switch back the exact same way, if you really want.

$ chsh -s /bin/zsh

You might want to re-login or close all of your terminals for the change to take effect.

___

___

## Install Oh-My-ZSH

Now that you have ZSH installed and enabled as your default shell, it’s a \*very\* good idea to pick up an add-on for ZSH, called Oh-My-ZSH. It’s a bundle of theme and plugins that enhance ZSH’s existing functionality. The won’t slow it down or get in the way, so grab that and install it.

$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

If you’d like to read more about it before installing, check out the project’s `https://github.com/robbyrussell/oh-my-zsh`.

## The Config File

Just like Bash has `.bashrc`, ZSH has `.zshrc`. It’s the single file that contains the configuration options for the shell, and you can use it to set aliases and customize runtime behavior. As of now, you actually have a nice set of defaults thanks to Oh-My-ZSH, which set up the file during its installation.

## Themes

ZSH supports theming the prompt. It comes with a few built-in themes, but they’re nowhere near as good as the ones that come with Oh-My-ZSH. You can take a look at what they look like on the `https://github.com/robbyrussell/oh-my-zsh/wiki/themes` Oh-My-ZSH Wiki.

To change your theme, open `.zshrc` and find the line below. Change the theme name to whichever one you want to try out.

ZSH\_THEME="robbyrussell"

## Plugins

Oh-My-ZSH also brought with it a mountain of plugins. It’d take way too long to cover them all here, so check out the `https://github.com/robbyrussell/oh-my-zsh/wiki/Plugins` Oh-My-ZSH Wiki for the whole list. Regardless of which other ones you pick, enabling `extract` and `z` is a good idea. Once again, your plugins are set with a line in `.zshrc`.

plugins=(git extract z)

## Tab Completion

Bash does have tab completion, but it’s weak at best. ZSH takes tab completion to a new level. Try typing `ls` followed by the name of a directory. After the name, press tab twice in quick succession. ZSH will automatically display the files and folders within the directory that you named. You can navigate through those directories using the arrow keys. Press enter on the one that you want to see, and run the command.

The same thing works with other commands too. Try it out with `cd`.

It’s not just directories that ZSH can complete with tab. It works with commands too. Try typing in `mk` and pressing tab twice. You’ll get the same type of menu with different commands that begin with `mk`.

## Directory Shorthand

Do you hate typing long directory paths? ZSH has a solution for that too. It supports it’s own version of shorthand that lets you type only the first couple of letters of each directory in the path. It will match them to the full path as best as it can. If it finds multiple results, it’ll display them for you to choose.

Try entering `$ ls /u/sh/ico` into the terminal and pressing tab. ZSH will expand it out to the full path to the shared icons directory.

## Aliases

This is a feature of Oh-My-ZSH, not the shell itself, but it’s still really convenient. Oh-My-ZSH comes with a pile of excellent aliases for everything form navigating directories to common programs like Git and Systemd. Again, there are more than there’s time to go over here, but here are some hightlights.

cd ../.. = ...
cd ../../.. = ....
mkdir -p = md
rmdir = rd
git add = ga
git add --all = gaa
git branch = gb
git commit -m = gcmsg
git checkout = gco
git pull origin currentbranch = ggpull
git push origin currentbranch = ggpush
systemctl start = sc-start
systemctl stop = sc-stop
systemctl status = sc-status
systemctl enable = sc-enable

If you want to check out the whole list, again the `https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet` wiki is your best bet.

___

___

## Z

`Z` actually isn’t part of ZSH or Oh-My-ZSH, it’s just enabled as a plugin by the latter. Even still, it easily fit’s in with the same usage style that ZSH allows. `Z` is a script that keeps track of frequently used and recent directories, so you can access them with a single work or combination of characters.

For example, if you had a folder at `/home/user/Pictures/photography/Canon/2017/pics`, and you use it all the time, you can use `Z` to shorten that drastically. With `Z` you’d use the following [linux command](chrome-extension://pcmpcfapbekmbjjkdalcgopdkipoggdi/linux-commands) to enter that directory.

$ z pics

Yeah, it’s that ridiculously easy.

## Kill Process Search

It can be a pain to kill an unresponsive process. First, you need to use `ps` to find the offending process. Then, you need to use `kill` and the selected process number. ZSH streamlines that process. Type in `kill` followed by the name, or part of the name, of the process or program that you want to kill. Then, use tab to tell ZSH to discover the process ID.

Use this one with a degree of caution, though. Say you want to kill an unresponsive Firefox, but you have Firejail running with another program. Typing `kill fire` might not get you what you’re looking for, typing `kill firefox` probably will. It’s also really not a good idea to play around with this one as root. You really don’t wan to enter something like `kill sys` and bring down PID 1.

## Command Specific History

Sometimes looking back through your command history is a giant pain. You need that one command that you wrote 20 lines ago because you’re not entirely sure what switches you used, and can’t seem to find it despite all reason. Well, ZSH supports command-specific history. So, if you know that the command you used was `du`, type in `du` and then start pressing the up arrow. You’ll only see your recent uses of the du command.

## Switch Search

While man pages are great, they’re not all that convenient when you’re just looking to write a one-off command real quick. Plus, there’s always a lot more there than a basic reference of the available switches. ZSH has an awesome feature that lets you search for switches as you write your command. Begin the command, write the dash associated with the switch, then press tab. ZSH will display the available options for you. Most of the time, it’ll ask you if you want it to display all of the items, press `y` to confirm.

## Globbiing

Have you ever used a wildcard character to search for something from the terminal?

$ ls -l \*.png

That’s a form of globbing. Globbing is essentially regular expressions for the shell. While Bash does support it, ZSH expands its globbing capabilities far beyond Bash.

Try typing this command into your `/home` directory using ZSH.

$ ls \*\*/\*

Yeah, that’s a lot of junk in your terminal. That command actually lists everything in your current directory as well as all subdirectories. You can use it to find specific file types too.

$ ls \*\*/\*.txt

That’s all of the `.txt` files in your `/home` directory.

You can specify a full file name too. Try using it to find all `README` files in your `/home` directory.

$ ls \*\*/README.\*

You can also search for words or phrases within the file names.

\## Starts with READ
$ ls \*\*/(READ)\*.\*
## Ends With READ
$ ls \*\*/\*(READ).\*
## Contains READ Anywhere
$ ls \*\*/\*(READ)\*.\*

That’s a really awkward way to list files. There are a couple of very easy ways to specify files and folders.

\# Files Only
$ ls \*\*/\*(.)
# Folders Only
$ ls \*\*/\*(/)

You can also specify one of a number of characters.

\# All files that start with A
$ ls \*\*/\[A\]\*(.)
# All files that start with A or a
$ ls \*\*/\[Aa\]\*(.)
# All Files that contain the number
$ ls \*\*/\*\[1\]\*(.)
# Any files that end in a vowel
$ ls \*\*/\*\[aeiouy\](.)

___

___

If you want to exclude a character or characters, you can do that too.

\# Files that don't start with A or a
$ ls \*\*/\[^Aa\](.)

You can search for ranges of letters also.

\# Files that end in a number
$ ls \*\*/\*<1-10>(.)

### Glob Qualifiers

There are other options that you can use to sort and filter the results of your search. These are called glob qualifiers, and they make searching through your files dead simple.

First, you can restrict by file size with `L`.

$ ls -lahS \*\*/\*(.Lm+250)

The example above only shows files files larger than 250MB in size order.

So, `L` restricts by size. It’s paired with `k`, `m`, and `g` to specify size units. Then, there is a positive or negative number to set a cutoff point and determine whether the results will be above or below that point.

Check out a few more.

\# List all files under 1GB by size
$ ls -lahS \*\*/\*(.Lg-1)
# List all files over 10MB by size
$ ls -lahS \*\*/\*(.Lm+10)
# List all files that start with a under 100MB by size
$ ls -lahS \*\*/\[a\]\*(.Lm-100)

There are also qualifiers to filter by modification and access. They are `m` and `a` respectively. They can be paired with `s`, `m`, `h`, `d`, `w`, and `M`. Those stand for seconds, minutes, hours, days, weeks, and months.

To list all files modified within he last week, try this.

$ ls -lah \*\*/\*(.mw-1)

The number in the statement signifies how many of the unit to look back. This would find all files modified in the last 3 days.

$ ls -lah \*\*/\*(.md-3)

There are other less common qualifiers to explore, and you can absolutely string them together to narrow your searches even more.

## Autocorrect

This last feature is just really nice. Everyone’s mistyped something and had to retype everything from scratch. It’s just plain annoying. ZSH tries to help. If ZSH detects a word that looks like a mistyped version of an actual command, it’ll ask you if you want to correct it and run the command, saving you the trouble of having to retype everything.

Give it a shot by creating a directory, the wrong way.

$ mdkir some-folder

ZSH to the rescue!

## Closing Thoughts

There it is, ZSH in all its glory. This isn’t something that you can read here and immediately know. It’s a tool that you can pick up right now, and use exactly like you would Bash. Then, you can start to try out different features and slowly integrate them into your usual habits.

Once you do start to grow accustomed to ZSH, you’ll realize just how much you like and rely on it. It’s nothing really revolutionary, but it provides all sorts of conveniences that you’ll probably wish you thought of or had years ago.