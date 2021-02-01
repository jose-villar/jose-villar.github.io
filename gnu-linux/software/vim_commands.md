- ``gi``: Go to the last position where the cursor was in insert mode

- **Sort lines by second column:**

          :%! column -t
          :%! sort -k2

- ``i_CTRL-R``: select a register to insert from.

- operatorfunc' 'opfunc' string: This option specifies a function to be called by the \|g@\| operator.

- g@{motion} Call the function set by the 'operatorfunc' option.

- Use "@@" to set the unnamed register, for example:

        let @@ = "example contents of the unnamed register"

- **v:count**: The count given for the last Normal mode command.

- Variables used inside a function are local unless prefixed by something like "g:", "a:", or "s:".

- When a function reaches ":endfunction" or ":return" is used without an argument, the function returns zero.

- There can be no comment after ":map", ":abbreviate", ":execute" and "!" commands (there are a few more commands with this restriction).

- The ':source' command reads Ex commands from a file line by line.  You will
have to type any needed keyboard input.  The ':source!' command reads from a
script file character by character, interpreting each character as if you
typed it.
