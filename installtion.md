# Before downloading
There are a few things that you should keep in mind before downloading any iso file:

- Always download the iso file from the official website, double check if the site is correct.
- After downloading, check sum the iso file for making sure that your iso is not corrupt or has not been tampered in anyway.
- Always install with minimal installation; this saves some of your time in debloating your system.

## basic setup

Setup date and time according to your needs. Use `ip`
fontsize or fonttype

## Paritioning
Choose the correct partitioning scheme for your requirements.
Keep root and home seperate so that you can expand one without needing to expand the whole system

Use fdisk for partitioning

Types of partitions to create:
- swap (max 4GB)
- /boot (1GB)
- /boot/efi (1GB)
- rest of it as /

## Assigning filesystems to each partition

/boot - A boot should be ext4 partition can be done using `mkfs.ext4 /dev/devicename`
/boot/efi - EFI must be a FAT32 parition
/ - This has a lots of flexibility in terms of filesystem

## Encrypting the disk

This should be done for the /
