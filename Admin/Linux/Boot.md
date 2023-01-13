## Boot (UEFI)
### GRUB
#### Get the default kernel used by GRUB2:
> `grubby --default-index`
OR
> `grubby --default-kernel`
#### Change the default bootloader to GRUB2:
> `grubby --set-default-index=0`
OR
> `grubby --set-default-kernel=$path_to_kernel_file`
- Kernel files are found here: `/boot/vmlinuz-<version>`
#### Update Grub2 configuration file
After making changes to `/etc/default/grub` you need to run `grub2-mkconfig` for changes to be written to the grub.cfg file.
* Fedora
> `sudo grub2-mkconfig -o $boot_partition/$boot_dir_name/fedora/grub.cfg`
- Find out where boot partition is mounted using `lsblk` or `df`
- e.g. if `/dev/sda1` is mounted at `/boot/efi` and there is subdirectory `EFI` under it, then:
> `sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg`

### Windows Boot Manager (BOOTMGR)
bootmgr.exe
> Windows Boot Manager (Bootmgr.exe) is Microsoft's proprietary Unified Extensible Firmware Interface (UEFI) application. It is loaded from the volume boot code of your device's hard drive, and it **enables you to set up the boot environment**