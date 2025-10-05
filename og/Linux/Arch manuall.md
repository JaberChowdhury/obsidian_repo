![[2025-10-04]]

### 🐧 Arch Linux Installation Guide (Step by Step)

---

## 1. Set Font

```bash
setfont ter-132n
```

### Available fonts to choose

1. ter-124n
2. ter-132n (good bold)

---

## 2. Connect to Internet

## Connect to the WIFI

```bash
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect "WiFIName"

```

➡️ Enter Password

➡️ `quit`

## or Connect to the Ethernet

```jsx
dhcpcd
```

Test connection:

```bash
ping archlinux.org

```

(Stop with `Ctrl + C`)

---

## 3. Partitioning with `cfdisk`

```bash
cfdisk

```

- Choose **label type → gpt**
- Choose **Free Space** for Arch Linux

Create partitions:

1. `New → 100M` (Boot Partition)
2. Select Free Space → `New → 8G` (Virtual RAM / Swap)
3. Select Free Space → `New → Rest` (Root `/`)

Then:

- `Write → yes → Enter`
- `quit`

Check partitions:

```bash
lsblk

```

---

## 4. Format the Partitions

```bash
mkfs.ext4 /dev/sda3      # Root (/)
mkfs.fat -F 32 /dev/sda1 # Boot (/boot/efi)
mkswap /dev/sda2         # Swap

```

---

## 5. Mount the Partitions

```bash
mount /dev/sda3 /mnt
mkdir -p /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
swapon /dev/sda2

```

✅ Verify with:

```bash
lsblk

```

---

## 6. Install Base System (No DE)

```bash
pacstrap /mnt base linux-lts linux-firmware sof-firmware base-devel grub efibootmgr nano networkmanager

```

---

## 7. Generate File System Table

```bash
genfstab /mnt
genfstab /mnt > /mnt/etc/fstab

```

---

## 8. Enter Installed System

```bash
arch-chroot /mnt

```

Set timezone:

```bash
ln -sf /usr/share/zoneinfo/Asia/Dhaka /etc/localtime
date
hwclock --systohc --localtime   # Dual Boot
# OR
hwclock --systohc               # Single Boot

```

---

## 9. Localization

Edit locales:

```bash
nano /etc/locale.gen

```

➡️ Uncomment: `en_US.UTF-8 UTF-8`

➡️ Save (`Ctrl+O → Enter → Ctrl+X`)

Generate:

```bash
locale-gen

```

Set locale:

```bash
nano /etc/locale.conf

```

Add:

```
LANG=en_US.UTF-8

```

---

## 10. Keyboard Layout (Optional)

```bash
nano /etc/vconsole.conf

```

Add:

```
KEYMAP=us

```

---

## 11. Set Hostname

```bash
nano /etc/hostname

```

➡️ Write your hostname

---

## 12. Set Root Password

```bash
passwd

```

---

## 13. Add a User

```bash
useradd -m -G wheel -s /bin/bash UserName
passwd UserName

```

---

## 14. Setup Sudo

```bash
EDITOR=nano visudo

```

➡️ Uncomment:

```
%wheel ALL=(ALL) ALL

```

Test:

```bash
su UserName
sudo pacman -Syu
exit

```

---

## 15. Enable Network Manager

```bash
systemctl enable NetworkManager
// start
systemctl start NetworkManager

```

---

## 16. Setup Bootloader

```bash
grub-install /dev/sda
grub-mkconfig -o /boot/grub/grub.cfg

// duel boot setup

sudo pacman -S os-prober ntfs-3g fuse3

nano /etc/default/grub
GRUB_DISABLE_OS_PROBER=false

sudo os-prober
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

```bash
exit

```

---

## 17. Before Reboot

```bash
umount -a
reboot

```

➡️ Login with **Username** & **Password**

---

## 18. Post-Install Check

```bash
ping archlinux.org
setfont -d

```

---

## 19. Desktop Environment (Optional)

➡️ Choose and install your preferred DE (GNOME, KDE, XFCE, etc.)

Finally:

```bash
reboot

```

---

✅ Done! Arch Linux installed 🎉

---

Do you want me to also make this into a **cheat sheet PDF** with nice headings, boxes, and highlighting so you can use it during install without scrolling too much?

[v2 (2)](https://www.notion.so/v2-2-262c77bb00a78075b422e6c3c739ad0d?pvs=21)