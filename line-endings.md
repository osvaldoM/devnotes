# CR, LF, CR LF, WTF?

__CR__ and __LF__ are control characters, respectively coded 0x0D (13 decimal) and 0x0A (10 decimal)

They are used to mark a line break in a text file. 
 - Windows uses two characters, the __CR LF__ sequence;
 - Unix and MacOS only use __LF__
 - The old MacOS (before-OSX MacIntosh) used __CR__.

### History
![image](https://www.londontypewriters.co.uk/wp-content/uploads/2016/08/Working-Imperial-Litton-200-Manual-Typewriter-Light-Blue-London-Typewriters-1.jpg)

__CR__ = Carriage Return and __LF__ = Line Feed, the two expressions have their roots in the old typewriters / TTY. __LF__ moved the paper up (but kept the horizontal position identical) and __CR__ brought back the "carriage" so that the next character typed would be at the leftmost position on the paper (but on the same line). __CR+LF__ did both, i.e. preparing to type a new line.

Many electric typewriters made carriage return to be another key on the keyboard instead of a lever. The key was usually labeled "carriage return", "return", or "power return". However, to improve the keyboard for non-English-speakers, the symbol __↵__ was introduced to communicate the combined carriage return and line feed action.
In modern computers.

As time went by, the physical semantics of the symbols were no longer applicable, and as memory and floppy disk space were limited, some OS designers decided to only use one of the characters, they just didn't communicate very well with one another ;-). As a result, different OS's use different symbols for line endings.

Most modern text editors offer options/settings etc. that allow the automatic detection of the file's end-of-line convention and to display it accordingly. In fact every major text editor automatically handles line endigs with the unsurprising exception of microsoft's notepad.

### How to know what EOL(End Of File) convention a file is using ?
Run `file akunamatata.txt`
For  CRLF the output should be similar to: 
![image](https://i.ibb.co/yf6JC0w/Selection-075.png).

### Changinf EOL
Install [dos2unix](https://waterlan.home.xs4all.nl/dos2unix.html), Or using package manager

    apt-get install dos2unix
    
Run either `dos2unix akunamatata.txt` or `unix2dos akunamatata.txt`


### How to prevent git from making noise about line endings when you run `git status` ?

In some cases git might show your files as modified due to the automatic EOL conversion done, for instance, when cloning a Unix-based EOL Git repo to a Windows-based one and vice-versa.

Word in the streets is that changing your git configuration to the following does the trick.

    git config --global core.autocrlf false
        
        
There is however, another configuration file on git that dictates how git will deal with EOL, and that's `.gitattributes`.

 > Git manages line endings on a per-repository basis by configuring a special .gitattributes file. This file is committed into the repository and overrides an individual's core.autocrlf setting, ensuring consistent behavior for all users, regardless of their Git settings
 
 Because `.gitattributes` has higher priority than .gitignore, you should always pay attention to it.
