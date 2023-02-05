# gentoo-dotfiles
### host
main: rogstrix GL503GE
second: thinkpadT420

My gentoo configuration per individual hosts + shared.

## preparation
## partition
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
## mount
## stage3
## chroot
# install
## timezone & locale
## portage 
## base packages
## tools
![300px-Larry-nefarius-v2 svg](https://user-images.githubusercontent.com/92778316/216841517-fdccdf1d-1e0f-4082-925f-855a9b737d1b.png)
