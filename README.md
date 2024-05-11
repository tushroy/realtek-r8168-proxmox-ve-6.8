# Realtek r8168 Driver for Proxmox VE Kernel version 6.8
Blacklist r8169 kernel driver for being loaded

    echo blacklist r8169 >> /etc/modprobe.d/blacklist-r8169.conf

Once all of this is completed we are going to update our GRUB to have some specific kernel parameters for our realtek driver

    sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX="r8168.aspm=0 r8168.eee_enable=0 pcie_aspm=off loglevel=3"/' /etc/default/grub

Run following commands to download from source and compile, install the driver:

    mkdir r8168_v3 && cd r8168_v3
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00-1.debian.tar.xz
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00.orig.tar.bz2
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00-1.dsc
    dpkg-source -x r8168_8.053.00-1.dsc
    cd r8168-8.053.00/
    dpkg-buildpackage
    dpkg -i ../r8168-dkms_8.053.00-1_all.deb

Or download the driver directly and install

    wget http://ftp.debian.org/debian/pool/non-free/r/r8168/r8168-dkms_8.053.00-1_all.deb
    dpkg -i r8168-dkms_8.053.00-1_all.deb

Curated and inspired from:
 - https://www.reddit.com/r/Proxmox/comments/1828z6o/proxmox_upgrade_broke_realtek_r8168_drivers/
 - https://github.com/nathanhi/r8168
 - https://forum.proxmox.com/threads/unable-to-install-r8168-dkms-for-realtek-nic.137727/
 - https://gist.github.com/SQLJames/fe6fcd5e819d864986ce2eff6ad350da
