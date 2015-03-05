# mkinitcpio-chkcryptoboot

## Introduction
Archlinux mkinitcpio hook to check if the bootloader was modified and warn the user to not enter his root device password. Based on chkboot.

This effectively makes the bootloader code tamper evident, while allowing the root luks device to be more tamper resistant, by demonstrating to the user that the bootloader was modified. This can only be used with a bootloader that knows how to unlock an encrypted boot partition, like GRUB with it's CRYPTODISK feature.

It does support both MBR bootloaders and UEFI bootloaders. In the case of UEFI, the ESP partition must be left unencrypted, and a separate encrypted boot partition must be created.

## Attacks
Your BIOS must be secured with a password, if it's possible. And you should disallow booting from other medias. Except, in the case of booting from a USB device to thwart an evil maid attack. In either case, if your BIOS is modified, It might trick you into booting from a compromised bootloader. This bootloader can try to change your boot partition, after it's decrypted, to make the initramfs hook not to run, try to boot another kernel, etc. In this case, there will be no warn and you will probably end up typing your root device password. If you use chkboot in conjunction with this hook it will probably detect the changes and warn you, after the fact. But, since the bootloader configuration, kernel and initramfs are kept in the encrypted boot partition, this kind of attack is much harder to accomplish, because the attacker does only have minimal information about the bootloader being used. It does not have information about bootloader menu entries, kernels being used, etc. The compromised bootloader would need to account for all these things.
