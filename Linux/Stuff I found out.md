# Anime
> To download bulk animes eps and stream anime there are 2 options

- [Anime-Kaizoku](https://animekaizoku.com/) (for downloading bulk anime)
- ani-cli (for downloading anime in bulk and streaming it)
	`ani-cli -d` run this and wait for the prompt to load , select anime , then range of episodes and done *(its kinda slow compared to animekaizoku cuz it doesnt utilise xtreme download manager)*

# .desktop files
> To add your own desktop entry (app shortcut) or modify it

```
/usr/share/applications
```
most of the desktop files are here , if you want to execute an application with a special command then create an executable

first create a `some_name.sh` file then do 
```
chmod +x some_name.sh
```

then the part where it says `Exec` of the desktop entry 
```
[Desktop Entry]
Name=ProtonVPN
Exec=protonvpn
Terminal=false
Type=Application
Icon=protonvpn-logo
StartupWMClass=Protonvpn
Comment=ProtonVPN GUI client
Categories=Network;
Keywords=vpn;
```
add replace it with the path to the `some_name.sh` you just made


# Backup 
> Use the BTRFS mode when backing up , it restores your system to the original state :D


# Reflector-simple
Its a gui app to make use reflector easily.


# Powerpill
Cli app to increase download speeds , its works like a charm :D with pacman


# To set an alias permanently 
Add the alias command to your `.zshrc` or `.bashrc`
```
alias pp='sudo powerpill'
```
this means `pp` can be used instead of `sudo powerpill`


# Reflector - simple
> Mofo stopped working for some reason so found this command to reinstall every package on the system which kinda fixes it 

```
sudo pacman -Syu $(pacman -Qq) 
```
