# mkinitcpio-chkcryptoboot
Archlinux mkinitcpio hook to check if the bootloader was modified and warn the user to not enter his root device password.

This effectively makes the bootloader code tamper evident, while allowing the root luks device to be tamper proof, by demonstrating to the user that the bootloader was modified. This can only be used with a bootloader that knows how to unlock an encrypted boot partition, like GRUB with it's CRYPTODISK feature.

It does support both MBR bootloaders and UEFI bootloaders. In the case of UEFI, the ESP partition must be left unencrypted, and a separate encrypted boot partition must be created.

