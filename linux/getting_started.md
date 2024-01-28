# Getting started

## Changing defaults

- Change default editor and browser at `/etc/environment`
- Change locale settings at `/etc/default/locale` and `/etc/locale.conf`

### Changing wallpaper in EndeavourOS

- Change lock screen wallpaper at
  `background=/usr/share/endeavouros/backgrounds/endeavouros-wallpaper.png`
  /usr/share/sddm/themes/endeavouros

- To override settings in the `theme.conf` configuration file, create a custom
  `theme.conf.user` file in the same directory. For example, to change the theme's
  background:

`/usr/share/sddm/themes/name/theme.conf.user`

    [General]
    background=/path/to/background.png

## Waybar

- Add user to `input` group, to use caps and num lock indicators in waybar.

      sudo usermod -aG input jose

## Music player

    systemctl --user enable mpd.service
    systemctl --user start mpd.service

## Zsh

yay zsh
yay zsh-syntax-highlighting
yay zsh-autosuggestions
chsh -s $(which zsh)

Ex: source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

1. p10k
   yay -S zsh-theme-powerlevel10k
   echo 'source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc

2. Hack font
   yay ttf-hack-nerd

3. File explorers
   yay lf
   yay ranger

4. Zsh config as main distros
   yay grml-zsh-config

5. Ttdr
   yay tldr

6. Night mode
   yay redshift
   yay gammastep

7. Screenshots
   yay flameshot
   yay grim
   yay slurp

8. Media player
   yay smplayer
   yay vlc

9. Docker
   yay docker

10. Telegram
    yay telegram-desktop

11. Discord
    yay discord

12. Screen recorder
    yay obs-studio
    yay wf-recorder

13. Image editor
    yay gimp
    yay swappy

14. Display keystrokes on the screen
    yay screenkey slop

15. Email client
    yay neomutt mutt-wizard abook lynx urlscan
    -- You need to set up an "App password" on your google account

16. Gparted
    yay gparted

17. Screen saver
    yay xscreensaver

18. Music player
    yay ncmpcpp mpd wildmidi timidity ueberzug
    mkdir -p ~/.config/mpd/playlists/
    yay mpdris2
    mkdir ~/.config/mpDris2
    cp /usr/share/doc/mpdris2/mpDris2.conf ~/.config/mpDris2/mpDris2.conf
    systemctl --user enable mpDris2.service

19. Fix tearing issues
    yay picom

20. Set wallpaper
    yay feh

21. Mute/unmute microphone
    yay pamixer

22. Firewall
    yay gufw

23. Images
    yay inkscape
    yay imv

24. Music editor
    yay audacity

25. Nvim
    yay neovim
    yay npm
    yay cmake

26. Wayland
    yay wev

27. Music tagger
    yay beets

28. Themeing
    yay qt5ct
    yay qt6ct
29. Minimalist PDF viewer
    yay zathura-pdf-mupdf
    yay zathura

    sudoedit /usr/share/applications/zathura.desktop

    [Desktop Entry]
    Type=Application
    Name=Zathura PDF Reader
    Comment=A lightweight PDF viewer
    Exec=zathura %f
    Icon=zathura
    Categories=Office;Viewer;
    MimeType=application/pdf;

    xdg-mime default zathura.desktop application/pdf:
    xdg-mime query default application/pdf

30. Torrent client
    yay aria2c

31. Screen sharing
    pacman -S xdg-desktop-portal-hyprland
    pacman -S xdg-desktop-portal-gtk
    https://gist.github.com/PowerBall253/2dea6ddf6974ba4e5d26c3139ffb7580

32. Command runner
    yay just

33. Smarter cd
    yay zoxide
    zoxide init zsh

34. Auto Mounting
    yay udiskie

35. Rich text editor
    yay abiword

36. System information
    yay fastfetch

37. Bluetooth
    sudo pacman -S blueman

38. Themeing
    sudo pacman -S gnome-themes-standard

39. Socat
    sudo pacman -S socat

40. Vim checkhealth
    sudo pacman -S ripgrep
    sudo pacman -S fd
    sudo pacman -S lazygit
    sudo pacman -S tree-sitter-cli
    sudo pacman -S texlive-latexextra
    sudo pacman -S biber
    sudo pacman -S texlive-binextra
    sudo pacman -S ruby
    sudo pacman -S python-pip
    sudo pacman -S python-pynvim
    gem install neovim
    sudo npm i -g neovim
    cpan Neovim::Ext
    sudo pacman -S cpanminus
    cpanm --local-lib=~/.local/share/perl5 local::lib
    <!-- Add the following line to .zshrc -->

    ```
    eval "$(perl -I ~/.local/perl5/lib/perl5 -Mlocal::lib=~/.local/perl5)"
    ```

41. Start ssh agent automatically and make sure that only one ssh-agent process
    runs at a time

```sh
sudo pacman -S keychain
# add this to your .zshrc
eval $(keychain --eval --quiet ~/.ssh/id_ed25519)
```
