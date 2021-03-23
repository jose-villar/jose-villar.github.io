# Vim Commands

## Normal Mode

- ``gi``: Go to the last position where the cursor was in insert mode
- `gqq`: Format current line
- `<C-u>` / `<C-d>`: Scroll up / down
- `f + <character>`: Find character in line
- ``<C-w-v>``: Split vertically
- `<C-w-s>`: Split horizontally
- `*` / `#`: Search for word under the cursor (forward/backwards)
- `m + {a-z}`: Set mark in current file, valid only within the file
- `m + {A-Z}`: Set file mark, valid between files
- `' + {a-zA-Z}`: Go to line where mark was set
- `<backtick> + {a-zA-Z}`: Go to line and column where mark was set
- `gg=G`: Fix indentation of current file
- `<C-A>` / `<C-X>`: Increase/decrease numeration
- `zR` and `zM`: Unfold all/fold all
- `H`, `M`, `L`: Set cursor position to high, middle or low in the screen
- `zz`, `zt`, `zb`: See current line at the top, middle or bottom of the screen
- `<C-g>`: Show total number of lines
- `g8`: Get ASCII code of character under the cursor
- `g<`: Show last output again
- `g&`: Replay last search
- `g_`: Go to the last non-blank character in a line and [count -1] lines
  downward
- `<C-w><C-o>`: Make the current window the only one on the screen
- `]c` / `[c`: Go to next/previous conflict
- `<C-f>`: Scroll down entire page
- `<C-b>`: Scroll up entire page
- `K`:  Run a program (`man` is the default) to lookup the word under the cursor.

## Insert Mode

- `<C-e>`, `<C-y>`: Insert text from line above or below in insert mode
- `<C-n>`: Open Vim autocompletion in insert mode
- `<C-k>`: insert a digraph. (See `:digraphs` or `:dig` for available options)
- `<C-r>`: insert contents from a register.

## Command Mode

### Built-in

- `:checkhealth`
- `:marks` and `:delmarks!`
- `:vim /<word>/g **/*`: Search for a word across multiple files. Use `:copen`,
  `:cnext`, `:cprev`
- `-12,-10co.`
- `:only`: Make the current window the only one on the screen
- `:ls`: list buffers
- `:put=range(1,10)`: Insert a list of numbers from 1 to 10


### External

- Sort lines by second column:

          :%! column -t
          :%! sort -k2

