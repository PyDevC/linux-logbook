sudo -s

setenforce 0
lsblk
fdisk /dev/vda
mkfs.fat -F 32 -n SYS /dev/vda1
mkfs.ext4 -F -L BOOT /dev/vda2
mkfs.btrfs -f -L ROOT /dev/vda3
mount /dev/vda3 /mnt
cd /mnt
btrfs subvolume create @
btrfs subvolume create @home
btrfs subvolume create @cache
btrfs subvolume create @log
btrfs subvolume create @images
btrfs subvolume create @.snapshots

mount -o compress=zstd,noatime,subvol=@ /dev/vda3 /mnt

mkdir -p /mnt/{boot,home,.snapshots,var/{log,cache,lib/libvirt/images}}

mount -o compress=zstd,noatime,subvol=@home /dev/vda3 /mnt/home
mount -o compress=zstd,noatime,subvol=@images /dev/vda3 /mnt/var/lib/libvirt/images
mount -o compress=zstd,noatime,subvol=@log /dev/vda3 /mnt/var/log
mount -o compress=zstd,noatime,subvol=@cache /dev/vda3 /mnt/var/cache
mount -o compress=zstd,noatime,subvol=@snapshots /dev/vda3 /mnt/.snapshots

mount /dev/vda2 /mnt/boot
mkdir /mnt/boot/efi
mount /dev/vda1 /mnt/boot/efi

lsblk

udevadm trigger
mkdir -p /mnt/{proc,sys,dev/pts}

mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -B /dev /mnt/dev
mount -t devpts pts /mnt/dev/pts

source /etc/os-release
export VERSION_ID=$VERSION_ID
printenv | grep -i version

dnf --installroot=/mnt --releasever=$VERSION_ID group install -y core --use-host-config
dnf --installroot=/mnt --releasever=$VERSION_ID -y install glibc-langpack-en --use-host-config

mv /mnt/etc/resolv.conf /mnt/etc/resolv.conf.bak
cp -L /etc/resolv.conf /mnt/etc

dnf install -y arch-install-scripts

genfstab -U /mnt >> /mnt/etc/fstab

chroot /mnt /bin/bash

mount -a
mount -t efivarfs efivarfs /sys/firmware/efi/efivars
fixfiles -f onboot

dnf install -y kernel grubby grub2-common grub2-tools grub2-tools-minimal grub2-efi-x64 efibootmgr efi-filesystem shim-x64 grub2-tools-efi fwupd grub2-tools-extra btrfs-progs mokutil

rm /boot/efi/EFI/fedora/grub.cfg 
rm /boot/grub2/grub.cfg

dnf reinstall -y shim-* grub2-efi-* grub2-common

ls /boot/efi/EFI/fedora

ls /boot/loader/entries

vi /etc/default/grub

efibootmgr 

efibootmgr -c -d /dev/vda -p 1 -L "Fedora (Custom)" -l \\EFI\\FEDORA\\SHIMX64.EFI

efibootmgr

grub2-mkconfig -o /boot/grub2/grub.cfg

rm -f /etc/locatime

systemd-firstboot --prompt
passwd

exit 
umount -n -R /mnt 

reboot
