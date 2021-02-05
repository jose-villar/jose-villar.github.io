- ``operatorfunc``: This option specifies a function (string) to be called by the ``g@`` operator.

- `g@{motion}`: Call the function set by the ``operatorfunc`` option.

- Use ``@@`` to set the unnamed register, for example:

        let @@ = "example contents of the unnamed register"

- ``v:count``: The count given for the last Normal mode command.

- Variables used inside a function are local unless prefixed by something like ``g:``, ``a:``, or ``s:``

- When a function reaches ``endfunction`` or ``return`` is used without an argument, the function returns zero.

- There can be no comment after ``map``, ``abbreviate``, ``execute`` and ``!`` commands.

- The ``:source`` command reads ``Ex`` commands from a file line by line.  You will have to type any needed keyboard input.  The ``:source!`` command reads from a script file character by character, interpreting each character as if you typed it.

- **Print the word under the cursor**: ``echo expand("<cword>")``

- ``i_CTRL-R``: select a register to insert from.

- Note that in line 28 ``noremap`` is used to avoid that any other mappings cause trouble.  Someone may have remapped ``call``, for example.  In line 24 we also use ``noremap``, but we do want ``<SID>Add`` to be remapped.  This is why ``<script>`` is used here.  This only allows mappings which are local to the script: ``map-<script>``  The same is done in line 26 for `noremenu`.

        24 noremap <unique> <script> <Plug>TypecorrAdd  <SID>Add
        ...
        28 noremap <SID>Add  :call <SID>Add(expand("<cword>"), 1)<CR>

- **Add a command**:

        38 if !exists(":Correct")
        39      command -nargs=1  Correct  :call s:Add(<q-args>, 0)
        40 endif

- ``unlet``: This is especially useful to clean up used global variables and script-local variables (these are not deleted when the script ends). Function-local variables are automatically deleted when the function ends.
