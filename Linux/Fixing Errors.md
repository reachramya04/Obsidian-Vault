# pip
**Error**
```bash
Traceback (most recent call last):
  File "/usr/bin/pip", line 33, in <module>
    sys.exit(load_entry_point('pip==20.3.4', 'console_scripts', 'pip')())
  File "/usr/bin/pip", line 22, in importlib_load_entry_point
    for entry_point in distribution(dist_name).entry_points
  File "/usr/lib/python3.9/importlib/metadata.py", line 524, in distribution
    return Distribution.from_name(distribution_name)
  File "/usr/lib/python3.9/importlib/metadata.py", line 187, in from_name
    raise PackageNotFoundError(name)
importlib.metadata.PackageNotFoundError: pip
```

**Fix**
install pip from `curl -O https://bootstrap.pypa.io/get-pip.py`  then
`python get-pip.py pip==version`

# HDD
> Couldn't write on the hdd

**Fix**
`chown path_to_hdd`

>HDD didnt show up sometimes , had to restart

**Fix**
`sudo nano /etc/fstab`
Edit the fstab file and add the UUID and mount it wherever you like :)

# system update
> corrupted packages problem 

**Fix**
`pacman -S archlinux-keyring`
then `sudo pacman -Syyu`
:D

# play-pause (media keys)
> media keys werent working

**Fix**
`yay -S playerctl`
then edit the openbox config in `/home/javetsm/.config/openbox/rc.xml`
changed the `mpc [command]` to `playerctl [command]`

# conflicting packages while updating 
> Got  a beeeg npm error which said smth smth "already exists in filesystem"

**Fix**
```bash
sudo pacman --overwrite "*" -Syu
```

This forces it to overwrite the packages , btw that `"*"` does something magic like so that `-Syu` runs too :D
[More about all this here](https://unix.stackexchange.com/questions/240252/pacman-exists-on-filesystem-error)



