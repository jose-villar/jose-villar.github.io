- ``gi``: Go to the last position where the cursor was in insert mode

- `gq`: format line

- **Sort lines by second column:**

          :%! column -t
          :%! sort -k2

- **Scroll up**: ``<C-U>``

- **Scroll down**: `<C-D>`

- **Find letter in line**: `f + <letter>`

- **Find letter backwards in line**: `F + <letter>`

- `-12,-10co.`

- **Split vertically**: ``<C-W-V>``

- **Split horizontally**:`<C-W-L>`

- **Search for word under the cursor**: `*` (forward) and `#` (backwards)

- **Mark**: `m + [a-z]` then go to it with `' + [a-z]`

- `:marks` and `:delmarks!`

- **Increase enumeration in visual mode**: `<C-A>`

- **Fix indentation**: `gg=G`

- `:checkhealth`

- Unfold all/fold all: `zR` and `zM`

- `H`, `M`, `L`: Set cursor position to high, middle or low in the screen

- **Search for a word across multiple files**: `:vim /blablabla/g **/*`
  Then use `:copen`, `:cnext`, `:cprev`

- **See current line at the top, middle or bottom of the screen**: `zz`, `zt`, `zb`

- **Insert text from line above or below in insert mode**: `<C-e>`, `<C-y>`
