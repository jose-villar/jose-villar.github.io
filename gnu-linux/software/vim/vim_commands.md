# Vim Commands

## Normal Mode

- ``gi``: Go to the last position where the cursor was in insert mode
- `gqq`: Format current line
- `<C-u>` / `<C-d>`: Scroll up / down
- `f + <character>`: Find character in line
- ``<C-W-V>``: Split vertically
- `<C-W-L>`: Split horizontally
- `*` / `#`: Search for word under the cursor (forward/backwards)
- `m + {a-z}`: Set mark in current file, valid only within the file
- `m + {A-Z}`: Set file mark, valid between files
- `' + {a-zA-Z}`: Go to line where mark was set
- `\\` + {a-zA-Z}`: Go to line and column where mark was set
- `gg=G`: Fix indentation of current file
- `<C-A>` / `<C-X>`: Increase/decrease numeration
- `zR` and `zM`: Unfold all/fold all
- `H`, `M`, `L`: Set cursor position to high, middle or low in the screen
- `zz`, `zt`, `zb`: See current line at the top, middle or bottom of the screen

## Insert Mode

- `<C-e>`, `<C-y>`: Insert text from line above or below in insert mode
- `<C-n>`: Open Vim autocompletion in insert mode

## Command Mode

- `:checkhealth`
- `:marks` and `:delmarks!`
- `:vim /<word>/g **/*`: Search for a word across multiple files. Use `:copen`,
  `:cnext`, `:cprev`

### Built-in

- `-12,-10co.`

### External

- Sort lines by second column:

          :%! column -t
          :%! sort -k2

