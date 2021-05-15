## Tmux shortcuts

Tmux is a terminal multiplexer. It lets us use a single environment to launch
multiple terminals, or windows, each running its own process or program.

Note: All listed functions listed below require Ctrl+b keyboard press key before 
Help:C-a ?

### Commands
```
tmux #new session
tmux kill-server && tmux #restart your tmux
tmux new-session -s basic or tmux new -s basic #new session with name
tmux list-sessions or tmux ls #list existing sessions
tmux attach or tmux a #attach if have one session.
tmux new -s snd_basic -d #new tmux instance in the background
tmux a -t snd_basic #attach to the session
tmux kill-session -t basic #Killing Sessions
tmux rename-session -t current-name new-name #rename a session
```

### Window Management
```
c #Create a new window
, #Rename current window
w #Get current window list
p #previous window
n #Move to previous window
[0-9] #Move to numbered window
f name #Search a window by name
& #Force a window to close
t #Show time
```

### Split
```
% #Horizontal screen cut
“ #Vertical screen cut
{ #Move to previous pane
} or o #Move to next pane.
o #Cycle through the open panes
q #Get panes numbers
! #Grow pane size
the UP , DOWN , LEFT , or RIGHT keys #to move around the panes
SPACEBAR #Cycles through the various pane layouts.
```

### History
```
PageUP #View upword in history
PageDown #View downward in history
```

### Session
```
d #Detach tmux session
s #List tmux session
( #Jump to next session
) #Jump to prevision sessions
x #Exit tmux session
$ #rename the current session
tmux new-session -s work2 -t work #Create a new session that shares all windows with an existing session
```

### Command Mode
```
: #to enter Command mode
new-window -n console #create a new window and give it a name using -n flag.
new-window -n processes “top” #new window appears with top command running
```
### Sync Panes
```
:setw synchronize-panes on
:setw synchronize-panes off
```
### Resizing Panes
```
resize-pane -D 10
resize-pane -U 10
resize-pane -L 10
resize-pane -R 10
```

```
.tmux.conf

set-option -g prefix C-q
unbind-key C-b
bind-key C-q send-prefix

#set history limit
set -g history-limit 20000

# Runtime reload
bind r source-file ~/.tmux.conf

# statusbar --------------------------------------------------------------

set -g display-time 2000

# default statusbar colors
set -g status-fg cyan
set -g status-bg default
set -g status-attr dim

# default window title colors
set-window-option -g window-status-fg black
set-window-option -g window-status-bg default
set-window-option -g window-status-attr dim

# active window title colors
set-window-option -g window-status-current-fg blue
set-window-option -g window-status-current-bg default
set-window-option -g window-status-current-attr bright

# command/message line colors
set -g message-fg black
set -g message-bg default
set -g message-attr bright

set -g status-interval 1
set -g status-justify centre
set -g status-left "[#[fg=green] #{pane_current_path} #[default]]"
set -g status-right "[ #[fg=magenta]#H #[default] ]"
#set -g status-right "[ #[fg=magenta]#(cat /proc/loadavg | cut -d \" \" -f 1,2,3)#[default] ][ #[fg=default]%a %Y-%m-%d %H:%M #[default]]"
set -g status-left-length 50
```


