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
- Use `:dv` to open 3 windows to compare the files.
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
