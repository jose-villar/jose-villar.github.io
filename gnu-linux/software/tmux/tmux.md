# Tmux

## Sessions

- `tmux ls`: List tmux sessions
- `tmux new -s <name>`: New session
- `tmux a -t <mySession>`: Attach a session
- `)`: Move to next session
- `(:` Move to previous session

## Visual Mode

- `[`: Enter visual mode
- `Ctrl + Spacebar`: Start selection
- `Ctrl + w`: Copy
- `Ctrl + ]`: Paste

## Panes

- `resize-pane -D 10`: Resize pane
- `z`: Zoom into a pane
- `q`: Show pane number
- `q + <number>`: Go to pane

## Windows

- `:swap-window -s 3 -t 1`: Swap windows 3 and 1
- `:swap-window -t 0`: Swap current window with the top window
