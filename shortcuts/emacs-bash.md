## Emacs - Shortcuts for Bash

### .bashrc
```
export PS1=$'\[\033[1;31m\]\u0905\u0936\u094b\u0915$ \[\033[00m\]'
PROMPT_COMMAND='history -a >(tee -a ~/.bash_history | logger -t “$USER[$$] $SSH_CONNECTION”)'
```

### Command Editing Shortcuts
```
Ctrl + a – go to the start of the command line
Ctrl + e – go to the end of the command line
Ctrl + k – delete from cursor to the end of the command line
Ctrl + u – delete from cursor to the start of the command line
Ctrl + w – delete from cursor to start of word (i.e. delete backwards one word)
Ctrl + y – paste word or text that was cut using one of the deletion shortcuts (such as the one above) after the cursor
Ctrl + xx – move between start of command line and current cursor position (and back again)
Alt + b – move backward one word (or go to start of word the cursor is currently on)
Alt + f – move forward one word (or go to end of word the cursor is currently on)
Alt + d – delete to end of word starting at cursor (whole word if cursor is at the beginning of word)
Alt + c – capitalize to end of word starting at cursor (whole word if cursor is at the beginning of word)
Alt + u – make uppercase from cursor to end of word
Alt + l – make lowercase from cursor to end of word
Alt + t – swap current word with previous
Ctrl + f – move forward one character
Ctrl + b – move backward one character
Ctrl + d – delete character under the cursor
Ctrl + h – delete character before the cursor
Ctrl + t – swap character under cursor with the previous one
```

### Command Recall Shortcuts
```
Ctrl + r – search the history backwards
Ctrl + g – escape from history searching mode
Ctrl + p – previous command in history (i.e. walk back through the command history)
Ctrl + n – next command in history (i.e. walk forward through the command history)
Alt + . – use the last word of the previous command
```

### Command Control Shortcuts
```
Ctrl + l – clear the screen
Ctrl + s – stops the output to the screen (for long running verbose command)
Ctrl + q – allow output to the screen (if previously stopped using command above)
Ctrl + c – terminate the command
Ctrl + z – suspend/stop the command
```

## Bash Bang (!) Commands

### Most important subset of band commands
```
!! – Will execute the last command. Same as !-1 or “up-arrow + return”
!n – Will execute the line n of the history record.
!-n – Will execute the command n lines back.
!gzip – will re-execute the most recent gzip command (history is searched in reverse order). string specified is considered to be prefix of the necessary command.
!?etc.gz – same as above but the unique string doesn't have to be at the start of the command. That means that you can identify command by a unique string appearing anywhere in the command (exactly like in Ctrl-R mechanism)
!!:1 or !!:^ – designates the first argument of the last command. This can be shortened to !1 or !^.
!!:$ – designates the last argument of the preceding command. This may be shortened to !$.
:p – suffix with the ! for repeating a command will cause the command to be displayed, but not run. Useful if you want to repeat a command, but want to double check the command you want to run. e.g !tail:p
```

### Retrieving previous command arguments
```
!:0 – is the previous command name.
!^, !:2, !:3, …, !$ – are the arguments of the previous command
!* or !:0-$ – is all the arguments
!$ – is the last argument. You can also use $_ to get the last argument of the previous command.
!-2, !-3, … – are earlier commands and arguments can be extracted from earlier commands too.
!:-2^ – First argument of second last command.
!-2:2 – second argument of second last command.
!-2$ – Last argument of second last command.
^foo^bar – Run the previous command replacing foo with bar
```

### Word Modifiers
```
h – remove the part of a filename after last “/”, leaving the path.
(for “/etc/resolv.conf” it will be /etc) e.g. last command is ll /etc/resolv.conf then echo !*:h, output will be /etc
t – remove all but the part of the filename after the last slash.
( for “/etc/resolv.conf” it will be resolv.conf) e.g last command is wget http://www.example.com/path/exmaple.tar.gz then mkdir !-2$:t:r:r ({creates directory called example)
r – remove the last suffix of a filename (extension of the file).
( for “/etc/resolv.conf” it will be r/etc/resolv)
e – remove all but the last suffix of a filename.
(for “/etc/resolv.conf” it will be .conf)
g – make changes globally, use with s modifier, below
p – print the command but do not execute it
q – quote the generated text
s/old/new/ – substitute new for old in the text. Any delimiter may be used. An & in the argument means the value of old. With empty old , use last old , or the most recent !? str ? search if there was no previous old
x – quote the generated text, but break into words at blanks and newline
& – repeat the last substitution
( instead of !!:s/myfile/myfile.old/ we can write !!:s/myfile/&.old/ )
```

### word designators
```
0 – the zero’th word (command name)
n – word n
ˆ – the first argument, i.e., word one (usually first argument of the command )
$ – the last argument
% – the word matched by the most recent
!? str ? – search of str
x-y – words x through y . −y is short for 0−y
* – words 1 through the last (like 1−$ ) (all arguments )
n* – words n through the last (like n−$
```

