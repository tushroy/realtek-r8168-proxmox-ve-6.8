
# Realtek r8168 Driver for Proxmox VE Kernel version 6.8
Run following commands:

    mkdir r8168_v3 && cd r8168_v3
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00-1.debian.tar.xz
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00.orig.tar.bz2
    wget http://deb.debian.org/debian/pool/non-free/r/r8168/r8168_8.053.00-1.dsc
    dpkg-source -x r8168_8.053.00-1.dsc
    cd r8168-8.053.00/
    dpkg-buildpackage
    dpkg -i ../r8168-dkms_8.053.00-1_all.deb
