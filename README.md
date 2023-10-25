# qemu-debian-buster


Qemu Debian Buster on Archlinux
```
sudo pacman -S qemu-common qemu-img qemu-system-x86
```
Install and launch Debian/buster image in qemu


Download the kernel:
```
$ wget http://ftp.debian.org/debian/dists/buster/main/installer-amd64/current/images/netboot/debian-installer/amd64/linux
```
Download an initrd:
```
$ wget http://ftp.debian.org/debian/dists/buster/main/installer-amd64/current/images/netboot/debian-installer/amd64/initrd.gz
```
Create a disk drive, that is a file image:
```
$ qemu-img create mydisk.img 10G
```
Run qemu and wait for installer to come up:
```
$ qemu-system-x86_64 -nographic -m 4G -hda test.img -kernel linux -initrd initrd.gz
```
Run in another window to see the screen:
```
$ vncviewer :5900
```

### Install

Run through the installer and set root and username user/password combination

hostname:debian
root/root
your_user/your_user

Selected Xfce to pick a slim window manager
Deselectd "print server" and selected "ssh server"
Accept grub boot loader on /dev/sda

### Launch

```
$ qemu-system-x86_64 -hda test.img -smp 4 -m 4G
```



Optional With some kvm acceleration:

check to see if it's in the kernel and drivers are loaded: 

```
$ lscpu | grep Virtualization
```
Virtualization:                     VT-x

```
$ lsmod | grep kvm
```
kvm_intel             393216  0
kvm                  1155072  1 kvm_intel
irqbypass              16384  1 kvm


And launch with kvm hypervisor (accelerator)
```
$ qemu-system-x86_64 -hda test.img -smp 4 -m 4G -accel kvm 
```



