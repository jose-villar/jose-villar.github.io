- Use `@@` to set the unnamed register, for example:

        let @@ = "example contents of the unnamed register"

  - `v:count`: The count given for the last Normal mode command.

  - Variables used inside a function are local unless prefixed by something like `g:`, `a:`, or `s:`

  - When a function reaches `endfunction` or `return` is used without an argument, the function returns zero.

  - There can be no comment after `map`, `abbreviate`, `execute` and `!` commands.

  - The `:source` command reads `Ex` commands from a file line by line. You will have to type any needed keyboard input. The `:source!` command reads from a script file character by character, interpreting each character as if you typed it.

  - **Print the word under the cursor**: `echo expand("<cword>")`

  - `i_CTRL-R`: select a register to insert from.

  - Note that in line 28 `noremap` is used to avoid that any other mappings cause trouble. Someone may have remapped `call`, for example. In line 24 we also use `noremap`, but we do want `<SID>Add` to be remapped. This is why `<script>` is used here. This only allows mappings which are local to the script: `map-<script>` The same is done in line 26 for `noremenu`.

          24 noremap <unique> <script> <Plug>TypecorrAdd  <SID>Add
          ...
          28 noremap <SID>Add  :call <SID>Add(expand("<cword>"), 1)<CR>

  -   **Add a command**:

          38 if !exists(":Correct")
          39      command -nargs=1  Correct  :call s:Add(<q-args>, 0)
          40 endif

  - `unlet`: This is especially useful to clean up used global variables and script-local variables (these are not deleted when the script ends). Function-local variables are automatically deleted when the function ends.

## Mapping An Operator `map-operator`

  An operator is used before a `{motion}` command. To define your own operator you must create mapping that first sets the `operatorfunc` option and then invoke the `g@` operator. After the user types the `{motion}` command the specified function will be called.

  `g@{motion}` Call the function set by the `operatorfunc` option. The `'[` mark is positioned at the start of the text moved over by `{motion}`, the `']` mark on the last character of the text. The function is called with one String argument: `line {motion}` was linewise `char {motion}` was characterwise `block {motion}` was blockwise-visual

  Although `block` would rarely appear, since it can only result from Visual mode where `g@` is not useful.

  Here is an example that counts the number of spaces with `<F4>`:

          nmap `<silent>`{=html} `<F4>`{=html} :set opfunc=CountSpaces`<CR>`{=html}g@ vmap `<silent>`{=html} `<F4>`{=html} :`<C-U>`{=html}call CountSpaces(visualmode(), 1)`<CR>`{=html}

          function! CountSpaces(type, ...) let sel_save = &selection let &selection = "inclusive" let reg_save = @@

              if a:0  " Invoked from Visual mode, use gv command.
                silent exe "normal! gvy"
              elseif a:type == 'line'
                silent exe "normal! '[V']y"
              else
                silent exe "normal! `[v`]y"
              endif

              echomsg strlen(substitute(@@, '[^ ]', '', 'g'))

              let &selection = sel_save
              let @@ = reg_save

          endfunction

  Note that the `selection` option is temporarily set to `inclusive` to be able to yank exactly the right text by using Visual mode from the \'\[ to the \'\] mark

## Replace a series of asterisk bullet points with a numbered list

        :let c=0 | g/^* /let c+=1 | s//\=c.'. '

First it initializes the variable `c` then it executes the global command `g` which looks for the pattern `^* `
Whenever a line containing this pattern is found, the global command executes the command `let c+=1 | s//\=c.'. '`
It increments the variable `c`, then it substitutes (`//`) with the evaluation of an expression (`\=`): the contents of variable `c` concatenated (.) with the string `'. '`

- If you don't want to modify all the lines from your buffer, but only a specific paragraph, you can pass a range to the global command. For example, to modify only the lines whose number is between 5 and 10:

        let c=0 | 5,10g/^* /let c+=1 | s//\=c.'. '

To make a command, you can use:

        command! -range=% NumberedLists let [c,d]=[0,0] | <line1>,<line2>g/^/let [c,d]=[line('.')==d+1 ? c+1 : 1, line('.')] | s//\=c.'. '

## Variables

The scope name by itself can be used as a Dictionary. For example, to delete
all script-local variables:

        :for k in keys(s:)
        :    unlet s:[k]
        :endfor

The behavior of `==` depends on a user's settings.

-  `==?` is the "case-insensitive no matter what the user has set" comparison operator
-  `==#` is the "case-sensitive no matter what the user has set" comparison operator.


