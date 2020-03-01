# manjaro-notes
### Fastest pacman
```
sudo pacman-mirrors --fasttrack 5
```
### Update Your System
```
sudo pacman -Syu
or 
pamac update
```

### Packages I use
```
sudo pacman -S yay aria2 speedtest-cli telegram-desktop kdenlive inkscape create_ap virtualbox fish flameshot deepin-terminal neofetch gtop kolourpaint gedit autoconf binutils make gcc pkg-config fakeroot libtool automake patch
```

### Remove Packages which I don't use gedit
```
sudo pacman -Rns kate
```
### Change the bash shell to fish
```
chsh -s /usr/bin/fish
curl -L https://get.oh-my.fish | fish
omf install bobthefish
```
## Customize shell and terminal
Change `.config/fish/conf.d/omf.fish` with [this](https://github.com/oguzkaganeren/manjaro-cinnamon-dell-7559/blob/master/.config/fish/omf.fish)
Set default deepin terminal then open it. Right click on the terminal and switch theme `argonaut`.

### Aur Packages I use
```
yay -S materia-theme opera chromium ttf-font-awesome ttf-font-awesome-4 ttf-roboto android-studio woeusb-git jdownloader2 ttf-ms-fonts vscodium-bin breeze-blurred-git otf-san-francisco xdman gwe svr zettlr-bin fslint waterfox-bin odio-appimage skypeforlinux-stable-bin posy-cursors all-repository-fonts ttf-wps-fonts performance-tweaks indicator-stickynotes
```
## Nvidia Options
**There are many options for installing nvidia driver. Follow the [link](https://forum.manjaro.org/t/options-for-nvidia-optimus-graphics/75185)**
### Power settings(optional)
About: https://forum.manjaro.org/t/howto-power-savings-setup-20180906/1445
### Change light-locker with betterlockscreen(optinal)
```
sudo pacman -Rns light-locker
yay -S betterlockscreen
cp /usr/share/doc/betterlockscreen/examples/betterlockscreenrc ~/.config
betterlockscreen -u /usr/share/backgrounds/wallpapers-2018/palm-wave.jpg
```
Set shortkey;
```
betterlockscreen -l dim
```
`Right click -> properties` on whisker menu(manjaro icon at bottom-left of the screen). Change lock screen command with `betterlockscreen -l dim` at Commands tab.
**Reset all keyboard shortcut Settings  →  Keyboard  (optionally)**
Add super key whiskermenu
```
xfce4-popup-whiskermenu
```
**Change show desktop shortcut Settings  →  Window Manager  →  Keyboard  → Show Desktop**
### Dual-boot Wrong time problem
```
timedatectl set-local-rtc 1 --adjust-system-clock
```
### Adblock Spotify
```
yay -S --mflags --skipinteg --needed spotify spotify-adblock
```

### SSD
>  :exclamation: If you have a SSD, you should enable fstrim.

```
sudo systemctl enable fstrim.timer
```
### Firefox screen tearing during scrolling Issue
```
sudo gedit /etc/profile.d/kwin.sh
```
then put this in it,
```
#!/bin/sh

export KWIN_TRIPLE_BUFFER=1
```
After that, 
```
sudo gedit ~/.config/kwinrc
```
Add those parameters at the bottom,

```
MaxFPS=60
RefreshRate=60
```
Save it and reboot. 
Open firefox and 
**about:config**
then search  **layers.acceleration.force-enabled**
It should be true.
Done.
### If skype not run
```
sudo sysctl kernel.unprivileged_userns_clone=1
```
### If headphones not detected when restart (after startup not working, I am working on it )
```
sudo nano /etc/pulse/default.pa
```
at the bottom under `### Make some devices default` put
```
set-default-sink 3
set-default-source 3
```
## Nvidia Options
**There are many options for installing nvidia driver. Follow the [link](https://forum.manjaro.org/t/options-for-nvidia-optimus-graphics/75185)**

### Open Wifi Hotspot
```
sudo create_ap wlp5s0 wlp5s0 MyAccessPoint password
```

#### Libre Office icon;
```
yay -S papirus-libreoffice-theme
```
After that;
LibreOffice->tools->options->View->Icon Style->Papirus

### Latte-Dock
If you want to panel which like first image, you should install latte-dock.
```
sudo pacman -S latte-dock
latte-dock
```
You can edit the dock with right click on it.(You can add programs shortcut with drag-drop.)
#### For shortcut(Windows key) for the dock
Right click on the dock and Layout>Plasma, then open terminal
```
kwriteconfig5 --file ~/.config/kwinrc --group ModifierOnlyShortcuts --key Meta "org.kde.lattedock,/Latte,org.kde.LatteDock,activateLauncherMenu"
qdbus org.kde.KWin /KWin reconfigure
```
Done. After that, you can open application launcher with Windows key.
### For Other Partitations
If you have another partition(E, D etc.). You can mount it on the startup. Thus some applications which are using other partitions don't get an error.

```
lsblk -f
```
The command shows your disks uuid.
```
sudo gedit /etc/fstab 
```
Open your fstab config with the command. You should add codes similar to the following example. You should change UUID and /run/media/yourUserName/Partition.
```
UUID=b336b98e-d0b5-4254-b6aa-9e66f85b0dfc /run/media/oguz/Files ext4 defaults  0 0
```

>  :exclamation: If you use manjaro with dual boot, you should close fast-startup,hibarnate on your Windows, otherwise, you have not a write permission for other partitions.
### Touchpad tap-to-click
sudo nano /etc/X11/xorg.conf.d/30-touchpad.conf  
```
Section "InputClass"
Identifier "touchpad"
Driver "libinput"
MatchIsTouchpad "on"
Option "Tapping" "on"
Option "NaturalScrolling" "off"
Option "DisableWhileTyping" "on"
Option "HorizontalScrolling" "on"
Option "Tapping" "on"
Option "TappingDrag" "on"
EndSection
```
#### For Android Studio(KVM);
```
sudo pacman -S virt-manager qemu vde2 ebtables dnsmasq bridge-utils openbsd-netcat
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service
```

yay -S candy-icons-git

git clone https://github.com/EliverLara/firefox-sweet-theme/ && cd firefox-sweet-theme
./scripts/install.sh -g

### Kernel 5.5 No Sound
Add following line to `/etc/modprobe.d/alsa.conf`

```
options snd-intel-dspcfg dsp_driver=1
```

### Android emulator sound problem
In `/etc/pulse/default.pa` change `load-module module-udev-detect` to `load-module module-udev-detect tsched=0`

and in `/etc/pulse/daemon.conf` change `; default-sample-rate = 44100 to default-sample-rate = 48000`

Finally restart pulseaudio with `pulseaudio -k`

### DVD/CD Mounting
If you have a external CD/DVD,
```
sudo pacman -S k3b
```

### Format USB with Terminal
```
sudo umount /dev/sdxx
sudo mkdosfs -F 32 -I /dev/sdxx
```
## For Developers
### Docker
```
sudo pacman -S docker-compose 
sudo usermod -aG docker oguz 
sudo systemctl start docker
sudo systemctl enable docker

reboot
```
### PostgreSQL
```
sudo pacman -S postgresql
sudo su postgres -l # or sudo -u postgres -i
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
sudo systemctl enable --now postgresql.service
sudo pacman -S pgadmin4

```
ERROR: Node.js version 11.15.0 is no longer supported.
sudo npm install -g n
sudo n latest

### Nvidia Overclock
```
sudo gedit /etc/X11/xorg.conf
```
Unlock everything under Nvidia X Server Settings gui including fan control and overclocking. Add this under both “Device” and “Screen” sections.
```
Option         "Coolbits" "31"

```
Also, enable TripleBuffer under the “Device” section.

By default TripleBuffer is disabled. This even in some cases can help load times with the driver and games.

```
Option 	   "TripleBuffer" "True"
```
To bypass PowerMizer and Adaptive Clocking add this under the “Device” section.
```
Option         "RegistryDwords" "PowerMizerEnable=0x1; PerfLevelSrc=0x3322; PowerMizerDefaultAC=0x1"
```

    PowerMizerEnable=0x1 turns on PowerMizer.
    PerfLevelSrc=0x2222 tells the video card to operate at full on both AC & battery.
    PowerMizerDefaultAC=0x1 tells the card to behave as if AC power is connected.
PerfLevelSrc=0x2222 is for desktops.

Source https://forum.level1techs.com/t/nvidia-gpu-settings-guide-for-better-performance/131660

## Change Default Java Version
```
sudo archlinux-java status
sudo archlinux-java set java-10-openjdk
```

### PostgreSQL
```
sudo pacman -S postgresql
sudo su postgres -l # or sudo -u postgres -i
initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data/'
exit
sudo systemctl enable --now postgresql.service
sudo pacman -S pgadmin4

```
## Some Errors and fixer
### Virtualbox
#### NS_ERROR_FAILURE (0x80004005) Error
```
Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
MachineWrap
Interface: 
IMachine {85cd948e-a71f-4289-281e-0ca7ad48cd89}
```
This is the error and we can fix it with this;
```
sudo pacman -Syyu
sudo pacman -S virtualbox-host-dkms
sudo pacman -S linux-headers
sudo modprobe vboxdrv
sudo /sbin/rcvboxdrv setup
```
#### VirtualBox: Error -610 in supR3HardenedMainInitRuntime!
This is the error.
```
VirtualBox: Error -610 in supR3HardenedMainInitRuntime!
VirtualBox: dlopen("/usr/lib/virtualbox/VBoxRT.so",) failed: <NULL>

VirtualBox: Tip! It may help to reinstall VirtualBox.
```
Maybe it can fix with(I didn't try it);
```
sudo chmod -002 /usr/lib/virtualbox
```
Or, I fix it with;
```
sudo chmod -002 /usr
```
## Stuck at hardware detection
>  :exclamation: When installing, It can be stuck at hardware detection. You can apply these settings. It does not appear the newer iso.
```
sudo gedit /lib/calamares/modules/mhwdcfg/main.py
```
edit it with this;
```
def run():
    """ Configure the hardware """
    
    mhwd = MhwdController()
    
    # return mhwd.run()
    return None # <- Add this and comment the above line
```
## Fix ERROR: Cannot find the strip binary required for object file stripping.
```
sudo sudo pacman -S binutils make gcc pkg-config fakeroot
```
