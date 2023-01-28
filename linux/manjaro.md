# Manjaro Linux

## Software Management

- To update the mirror list use the following command:

        sudo pacman-mirrors -f 0

- Install a package:

        sudo pacman -S <package>

- Search for a package:

        sudo pacman -Ss <package>

- Force package list synchronisation and update:

        sudo pacman -Syyu
        sudo pamac upgrade
