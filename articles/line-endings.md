---
title: "CR, LF, CR LF, WTF?"
published: 2018-12-20
updated: 2021-02-09
summary: "Ever get confused when git complains about line endings not being normalized? In this article I explain what are the different types of line endings how to prevent git from making noise about them."
tags: [ 'os', 'git' ]
---

__CR__ and __LF__ are control characters, respectively coded 0x0D (13 decimal) and 0x0A (10 decimal). They are used to mark a line break in a text file. 

 - Windows uses two characters, the __CR LF__ sequence;
 - Unix and MacOS only use __LF__
 - The old MacOS (before-OSX MacIntosh) used __CR__.

## History

![image](https://www.londontypewriters.co.uk/wp-content/uploads/2016/08/Working-Imperial-Litton-200-Manual-Typewriter-Light-Blue-London-Typewriters-1.jpg)

__CR__ = Carriage Return and __LF__ = Line Feed, the two expressions have their roots in the old typewriters / TTY. __LF__ moved the paper up (but kept the horizontal position identical) and __CR__ brought back the "carriage" so that the next character typed would be at the leftmost position on the paper (but on the same line). __CR+LF__ did both, i.e. preparing to type a new line.

Many electric typewriters made carriage return to be another key on the keyboard instead of a lever. The key was usually labeled "carriage return", "return", or "power return". However, to improve the keyboard for non-English-speakers, the symbol __↵__ was introduced to communicate the combined carriage return and line feed action.
In modern computers.

As time went by, the physical semantics of the symbols were no longer applicable, and as memory and floppy disk space were limited, some OS designers decided to only use one of the characters, they just didn't communicate very well with one another ;-). As a result, different OS's use different symbols for line endings.

Most modern text editors offer options/settings etc. that allow the automatic detection of the file's end-of-line convention and to display it accordingly. In fact every major text editor automatically handles line endigs with the unsurprising exception of microsoft's notepad.

## How to know what EOL(End Of File) convention a file is using ?
Run:

```bash
file akunamatata.txt
```
For  CRLF the output should be similar to: 

```shell
$ file akunamatata.txt    
akunamatata.txt: ASCII text, with CRLF line terminators
```

## Changing EOL convention
Install [dos2unix](https://waterlan.home.xs4all.nl/dos2unix.html), Or using package manager

```bash
apt-get install dos2unix
```

Run either: 

```bash
dos2unix akunamatata.txt
``` 
or: 
```bash
unix2dos akunamatata.txt
```


## How to prevent git from making noise about line endings when you run `git status` ?

In some cases git might show your files as modified due to the automatic EOL conversion done, for instance, when cloning a Unix-based EOL Git repo to a Windows-based one and vice-versa.

Word in the streets is that changing your git configuration to the following does the trick.

```bash
git config --global core.autocrlf false
```
There is however, another configuration file on git that dictates how git will deal with EOL, and that's `.gitattributes`.

 > Git manages line endings on a per-repository basis by configuring a special .gitattributes file. This file is committed into the repository and overrides an individual's core.autocrlf setting, ensuring consistent behavior for all users, regardless of their Git settings  
 > -- <cite>[github manual on line endings][1]</cite>
 
 Because `.gitattributes` has higher priority than .gitignore, you should always pay attention to it.
 
 
 
 ## Refferences

1. : [https://en.wikipedia.org/wiki/Unix2dos](https://en.wikipedia.org/wiki/Unix2dos)

2. : [github manual on line endings](https://help.github.com/articles/dealing-with-line-endings/)

3. : [https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types](https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types)
   
4. : [https://stackoverflow.com/questions/20496084/git-status-ignore-line-endings-identical-files-windows-linux-environment](https://stackoverflow.com/questions/20496084/git-status-ignore-line-endings-identical-files-windows-linux-environment)
    
5. : [dos2unix tool](https://waterlan.home.xs4all.nl/dos2unix.html)
  https://luispuerto.net/blog/2020/01/04/normalize-line-endings-files-git/
