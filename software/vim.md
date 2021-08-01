# Vim Plugins

## Coc

        :CocInstall coc-marketplace coc-eslint coc-tsserver coc-json coc-html coc-css coc-python coc-phpls
        :CocList marketplace

## Fugitive

### Commit by hunks

- Use `:G` to open fugitive's git status.
- Use `:Gdiff` to open the index and working copies of the file side by side.
- Use `:diffget` and `:diffput`, to modify the contents of the files by hunks.
- Save the index file and the git status window will update.

### Merge conflicts

- Use `:G` to open figitive's git status.
- Use `:G merge <merge branch>`
- Place your cursor over a conflicting file
- Use `:dv` to open up 3 windows to compare the files.
- Use the custom mappings below to pick the changes

        "Press dv on the file that has merge conflicts, in the status menu
        "Target branch (active branch):2
        nmap <Leader>dg2 :diffget //2<BAR>:diffupdate<CR>
        "Merge branch (named in the git merge command):3
        nmap <Leader>dg3 :diffget //3<BAR>:diffupdate<CR>

### Rebasing

~~~
G log
// Place your cursor over a commit and then press ri
~~~

## Signify

- Use `[c` and `]c` to jump through chunks.
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
- `:find /<filename>:` Go to another file
- `:vim /<word>/g /*`: Find a word inside the files
- Search and replace in multiple files:
~~~
// the j flag is to prevent Vim from jumping to the first match immediately
:vimgrep/<word>/gj **/*
:cfdo %s/<word>/<newWord>/g | update
// you can use :copen to navigate through the quickfix list
~~~

### External

- Sort lines by second column:

          :%! column -t
          :%! sort -k2

