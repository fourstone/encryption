### Linux installation with Installer

## Ubuntu 18.04.1 LTS
somehow they have a couple of bugs in their installer, so what I did was the following:
- install encrypted with xfs root and ext4 boot partition. no swap partition (as that threw the error)
When the system was running:
- booted up, 
- installed refind
- mounted efi partition as /esp
- killed the content of the EFI/UBUNTU folder and linked that folder in as boot (bind mount via fstab)
- had refind create a refind config in /boot
- created a new luks partition, entered that in /etc/crypttab, made it swap
- opened the LXHOME luks device, also entered in fstab and crypttab
- set root password, logged in as root, logged out personal user
- switched home to folder in LXHOME, killed oldhome
- kept bootold for the time being, sometimes ubuntu needs that for upgrading etc.

and right, couple more things:
- installed gnome to have a proper gnome session
- uninstalled amazon (ubuntu-web-launchers)
- amdgpu-pro
