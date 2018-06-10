# motherfucking-nvidia-ubuntu-xps-9570

Motherfucking kill yourselves Dell / Nvidia. Also, Canonical.

## Setup

1. Disable a bunch of shit using `systemctl disable gpu-manager` and other stuff like that (fallback to nouveau, etc).
1. Blacklist and alias nouveau (`apt install nvidia-390` should do it for you)

## Boot Intel

```sh
rm /etc/modprobe.d/blacklist-nvidia.conf
echo blacklist nvidia >> /etc/modprobe.d/blacklist-nvidia.conf
echo blacklist nvidia_uvm >> /etc/modprobe.d/blacklist-nvidia.conf
echo blacklist nvidia_drm >> /etc/modprobe.d/blacklist-nvidia.conf
echo blacklist nvidia_modeset >> /etc/modprobe.d/blacklist-nvidia.conf
echo blacklist nvidia-current >> /etc/modprobe.d/blacklist-nvidia.conf
sudo cp /etc/X11/xorg.intel /etc/X11/xorg.conf
sudo rm /usr/share/X11/xorg.conf.d/20-intel.conf
[...add nouveau.runpm=0 and nomodeset to grub cmdline...]
sudo update-initramfs -u
sudo update-grub
```

## Boot NVIDIA

```sh
rm /etc/modprobe.d/blacklist-nvidia.conf
sudo cp /etc/X11/xorg.nvidia /etc/X11/xorg.conf
sudo rm /usr/share/X11/xorg.conf.d/20-intel.conf
[...remove nouveau.runpm=0 and nomodeset to grub cmdline...]
sudo update-initramfs -u
sudo update-grub
```
## Motherfucking LCD backlight

```sh
[grub cmd line] acpi_backlight=vendor
```
