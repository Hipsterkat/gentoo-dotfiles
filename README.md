# gentoo-dotfiles
My gentoo configuration per individual hosts + shared.
### hosts
1) ROGstrix GL503GE
2) Thinkpad T420

## reference guides
[base](https://wiki.gentoo.org/wiki/Handbook:AMD64/Installation/Base)
[mirrors](https://www.gentoo.org/downloads/mirrors)
[downloads](https://www.gentoo.org/downloads)
[handbook](https://wiki.gentoo.org/wiki/Handbook:Main_Page)
## partition
```
/dev/sda1 /mnt/gentoo/boot/efi
/dev/sda2 swap
/dev/sda3 /mnt/gentoo

mkfs.fat -F 32 /dev/sda1
mkswap /dev/sda2
mkfs.ext4 /dev/sda3
```
## stage3
```
# wget stage3.tar.xz
# tar xpvf stage3-*.tar.xz --xattrs-include='*.*' --numeric-owner
```
## fstab
```
# UUID=9e257225-61a2-460d-9c28-6620d043aaea
/dev/sda3           	/         	ext4      	rw,relatime	0 1

# UUID=EA01-74C7
/dev/sda1           	/boot/efi 	vfat      	rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro	0 2

tracefs             	/sys/kernel/tracing	tracefs   	rw,nosuid,nodev,noexec	0 0

# UUID=a856413a-8eeb-4325-bb30-836f5561c107
/dev/sda2           	none      	swap      	defaults  	0 0

```
## mount & chroot
```
# mount --types proc /proc /mnt/gentoo/proc & mount --rbind /sys /mnt/gentoo/sys & mount --rbind /sys /mnt/gentoo/sys 
& mount --make-rslave /mnt/gentoo/sys & mount --rbind /dev /mnt/gentoo/dev & mount --make-rslave /mnt/gentoo/dev &
mount --bind /run /mnt/gentoo/run & mount --make-slave /mnt/gentoo/run 
```
optional, incase gentoo is being installed in a live enviorment
```
# test -L /dev/shm && rm /dev/shm && mkdir /dev/shm & mount --types tmpfs --options nosuid,nodev,noexec shm /dev/shm 
& chmod 1777 /dev/shm /run/shm
```
chroot
```
# chroot /mnt/gentoo /bin/bash
# source /etc/profile
```

## timezone & locale
```
$ echo "Europe/Bucharest" > /etc/timezone
$ emerge --config sys-libs/timezone-data
$ nano -w /etc/locale.gen

en_US ISO-8859-1
en_US.UTF-8 UTF-8

$ locale-gen
$ eselect locale list
Available targets for the LANG variable:
  [1]   C
  [2]   en_US
  [3]   en_US.iso88591
  [4]   en_US.utf8
  [5]   POSIX
$ eselect locale set 4
$ env-update
$ source /etc/profile
$ cat LANG=en_US.UTF-8 > /etc/locale.conf
```
## portage 
```
COMMON_FLAGS="-march=native -O2 -pipe"
CFLAGS="${COMMON_FLAGS}"
CXXFLAGS="${COMMON_FLAGS}"
FCFLAGS="${COMMON_FLAGS}"
FFLAGS="${COMMON_FLAGS}"

USE="X wayland -cups gnome -kde -dvd -dvdr -systemd elogind dbus gtk3 pulseaudio alsa"
PYTHON_TARGETS="python3_6 python3_7 python3_8 python3_9 python3_10"
FEATURES="parallel-install unmerge-orphans"

VIDEO_CARDS="intel i915"
CHOST="x86_64-pc-linux-gnu"

GENTOO_MIRRORS="https://mirror.leaseweb.com/gentoo/"

ACCEPT_KEYWORDS="~amd64"
ACCEPT_LICENSE="-* @FREE"

EMERGE_DEFAULT_OPS="--jobs 5"
MAKEOPTS="-j4"

LC_MESSAGES=C
```
### update @world
```
# emerge-webrsync
# emerge -avuND @world
```
## base packages
```
# emerge 
```
## tools
```
# emerge 
```
![300px-Larry-nefarius-v2 svg](https://user-images.githubusercontent.com/92778316/216841517-fdccdf1d-1e0f-4082-925f-855a9b737d1b.png)
