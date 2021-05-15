## Vim Cheatsheet

### Help

```
“:help” and “:help command”
TAB - cycles through possible command completions
CTRL-d - lists possible command completions
For example
:help tags (then CTRL-d and TAB)
Do help i_ CTRL-d for insert commands, v_ for visual, etc.
Also, when in the help pages, CTRL-] jumps to subjects between |bars| and CTRL-T jumps back (and, of course, :q to quit).
```

### variables
```
:set - shows vars different from defaults
:set all - shows all values
:set foo? - shows the value of foo
:set foo+=opt - add opt to the value w/o changing others
:set foo-=opt - remove opt from value
:set foo& - reset foo to default value
:setlocal foo - only the current buffer
:verbose set foo? - tells you where it was last set!
```

### word & line completion
```
ctrl-n, ctrl-p - next/previous word completion (similar word in current file)
ctrl-x ctrl-l (ctrl-n/p) - line completion
:set dictionary=/usr/share/dict/words
ctrl-x ctrl-k - dictionary completion
ctrl-w - erases word (insert mode or on command line)
ctrl-u - erases line (insert mode or on command line)
```

### Searching
```
/pattern - search forward
?pattern - search backword
n - repeat forward search
N - repeat backword search
```

### Searching tricks
```
* - search for word currently under cursor.
g* - search for partial word under cursor .
ctrl-o, ctrl-i - go through jump locations
[I - show lines with matching word under cursor
```

### Some variables you might want to set:
```
:set ignorecase - case insensitive
:set smartcase - use case if any caps used
:set incsearch - show match as search proceeds
:set hlsearch - search highlighting
```

### text selection
```
V - selects entire lines
v - selects range of text
ctrl-v - selects columns
gv - reselect block
```
After selecting the text, try d to delete, or y to copy, or :s/match/replace/, or :center, or !sort

markers
Use markers to set places you want to quickly get back to, or to specify a block of text you want to copy or cut.
```
mk - mark current position (can use a-z)
'k - move to mark k
d'k - delete from current position to mark k
'a-z - same file
'A-Z - between files
```

### indenting
Some variables you might want to set:
```
:set tabstop 8 - tabs are at proper location
:set expandtab - don't use actual tab character (ctrl-v)
:set shiftwidth=4 - indenting is 4 spaces
:set autoindent - turns it on
:set smartindent - does the right thing (mostly) in programs
:set cindent - stricter rules for C programs
```
To indent the current line, or a visual block:
```
ctrl-t, ctrl-d - indent current line forward, backwards insert mode.
visual(V or v) and > or < - indent block by sw (repeat with . )
```
reformatting
These are useful to reformat text paragraphs or chunks of code:
```
V= - select text, then reformat with =
= - will correct alignment of code
== - one line;
gq - reformat paragraph
```

Options to change how automatic formatting is done:\
:set formatoptions (default “tcq”)
```
t - textwidth
c - comments (plus leader – see :help comments)
q - allogw 'gq' to work
n - numbered lists
2 - keep second line indent
1 - single letter words on next line
r - (in mail) comment leader after
```

Other related options:
```
:set wrapmargin
:set textwidth
```

### multiple windows
```
:e filename - edit another file
:split filename - split window and load another file
ctrl-w up arrow - move cursor up a window
ctrl-w ctrl-w - move cursor to another window (cycle)
ctrl-w_ - maximize current window
ctrl-w= - make all equal size
10 ctrl-w+ - increase window size by 10 lines
:vsplit file - vertical split
:sview file - same as split, but readonly
:hide - close current window
:only - keep only this window open
:ls - show current buffers
:b 2 - open buffer #2 in this window
```

### editing in a stream
You can take the output of any command and send it into a vim session. From there you could format it, change stuff, and then save it to a file.
find . | vim -

### tags
Using tags makes it easier to jump to certain parts of your programs. First run ctags from the UNIX command line on your source files (e.g., ctags prog.c or ctags -R to recurse) to generate a “tags” file, then use these while editing your source files:

```
:tag TAB - list the known tags
:tag function_name - jump to that function
ctrl-t - goes to previous spot where you called :tag
ctrl-] - calls :tag on the word under the cursor
:ptag - open tag in preview window (also ctrl-w })
:pclose - close preview window
```

### registers
When you copy and cut stuff, it gets saved to registers. You can pull stuff from those registers at a later time.

```
:reg - show named registers and what's in them
“5p - paste what's in register “5
```
You can also record a whole series of edits to a register, and then apply them over and over.

```
qk - records edits into register k (q again to stop recording)
@k - execute recorded edits (macro)
@@ - repeat last one
5@@ - repeat 5 times
“kp - print macro k (e.g., to edit or add to .vimrc)
“kd - replace register k with what cursor is on
```
