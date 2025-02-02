# Linux Quirks
Here i document some quirks i had, using linux as my daily driver and gaming-pc.
For this i've used nobara-linux.

I take no responsibility for the correctness of the commands.
Use at your own risk.

## Optical Drive Recognition
My optical drive was initially not recognized by applications.

```shell
su root
# Enter your Password
echo sg > /etc/modules-load.d/sg.conf
Exit
Reboot
```

Also, add user to `cdrom`-group.

```shell
sudo usermod -aG cdrom $USER
# Logout and login
```

Refer to 
* https://forum.makemkv.com/forum/viewtopic.php?f=3&t=16939&sid=be64f97bf489468b4690addecb339fe3&start=105

## Grub-Theming
Grub2 can be customized using https://github.com/vinceliuice/grub2-themes.

In `/etc/default/grub` set `GRUB_TERMINAL_OUTPUT` to `gfxterm` and rebuild the config grub:

```shell
sudo grub2-mkconfig
```

Refer to
* https://github.com/vinceliuice/grub2-themes
* https://askubuntu.com/questions/1288580/sudo-grub2-mkconfig-command-not-found
* https://www.reddit.com/r/Fedora/comments/5s62yc/grub_themes_not_working/


## 1Password Quick-Access
By default, quick-access using (Ctrl + Space) does not work under KDE + Wayland.
In order to work, we need to configre a global hotkey.
Go to `System Settings > Keyboard > Shortcuts` and add bind the command `1password --quick-access` to your desired hotkey(s).

## Black Screen after Suspend/Hibernate (NVIDIA)
Add the following line to `/etc/modprobe.d/nvidia-modset.conf`:
```text
options nvidia NVreg_PreserveVideoMemoryAllocations=1
```
