In Thinkpad Setup
=================

	Config
		Keyboard/Mouse
			Fn and Ctrl Key swap Enabled
		Beep and Alarm
			Keyboard Beep Disabled
	Startup
		UEFI/Legacy Boot
			UEFI/Legacy Boot Priority
				UEFI First

Press F12 for Boot Device List; point current boot device to the one
which has the Arch Linux installation medium.

In Live Installation Environment
================================

Connect to the internet with iwctl and check the connection with ping.

	ls /sys/firmware/efi/efivars

	timedatectl set-ntp true

	lsblk		# Choose which device to partition
	parted /dev/sda	# Replace /dev/sda with the chosen device
	# Interactively:
	# mklabel gpt
	# mkpart "EFI system partition" fat32 1MiB 261MiB
	# set 1 esp on
	# mkpart "root partition" ext4 261MiB 100%

	mkfs.fat -F32 /dev/sda1
	mkfs.ext4 /dev/sda2

	mount /dev/sda2 /mnt
	mkdir /mnt/efi
	mount /dev/sda1 /mnt/efi

	pacstrap /mnt base linux linux-firmware	\
		 vim man-db man-pages texinfo

	genfstab -U /mnt >>/mnt/etc/fstab

	arch-chroot /mnt

	ln -sf /usr/share/zoneinfo/UTC /etc/localtime
	hwclock --systohc

	sed -i '/#en_US.UTF-8 UTF-8/s/#//' /etc/locale.gen
	sed -i '/#ja_JP.UTF-8 UTF-8/s/#//' /etc/locale.gen
	locale-gen
	echo 'LANG=en_US.UTF-8' >/etc/locale.conf

	echo 'sakura' >/etc/hostname
	cat <<EOF >/etc/hosts
	127.0.0.1	localhost
	::1		localhost
	127.0.0.1	sakura.localdomain	sakura
	EOF
	pacman -S networkmanager
	systemctl enable NetworkManager.service

	passwd
	# Enter password

	pacman -S grub efibootmgr intel-ucode
	grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=GRUB
	grub-mkconfig -o /boot/grub/grub.cfg

	exit
	reboot

As Root
=======

Connect to the internet with nmcli.

	useradd -m ppsqkk
	passwd ppsqkk
	# Enter password

	sed -i '/#\[multilib\]/,+1s/#//' /etc/pacman.conf
	pacman -S sudo tlp clamav
	EDITOR=vim visudo
	# The sudoers file should contain the following:
	# ppsqkk ALL=(ALL) ALL
	#
	# @includedir /etc/sudoers.d
	systemctl enable tlp.service clamav-freshclam.service

	exit

As Non-Privileged User
======================

	sudo pacman -S git
	mkdir proj
	cd proj
	git clone https://github.com/ppsqkk/bin.git
	ln -s ~/proj/bin ~/bin
	git clone https://github.com/ppsqkk/backup.git
	cd backup
	sudo pacman -S - <pkglist.txt
	rm ~/.bash_profile
	./symdot
	exit

	~/proj/backup/symdot
	# Get data backup
	mkdir "$(xdg-user-dir DOWNLOAD)/vg"
	gpg --import "$(xdg-user-dir DESKTOP)/privkey.asc"
	gpg --encrypt --output ~/.msmtp-gmail.gpg --recipient kipling.i.liu@gmail.com -
	reboot

GUI Configuration
=================

IBus
----

In Setup - IBus-Anthy

	General
		Initial Setting
			Input Mode: Hiragana
	Key Binding
		circle_input_mode: [Ctrl+less]
		circle_kana_mode: [Ctrl+greater]
		hiragana_mode: [Ctrl+comma]
		katakana_mode: [Ctrl+period]

Snes9x
------

In Snes9x Preferences:

	Files
		SRAM: "$(xdg-user-dir DOWNLOAD)/vg"
		Save states: "$(xdg-user-dir DOWNLOAD)/vg"
		Cheats: "$(xdg-user-dir DOWNLOAD)/vg"
		Patches: "$(xdg-user-dir DOWNLOAD)/vg"
		Exports: "$(xdg-user-dir DOWNLOAD)/vg"

mGBA
----

In Settings:

	Paths
		Save games: "$(xdg-user-dir DOWNLOAD)/vg"
		Save states: "$(xdg-user-dir DOWNLOAD)/vg"
		Screenshots: "$(xdg-user-dir DOWNLOAD)/vg"
		Patches: "$(xdg-user-dir DOWNLOAD)/vg"
		Cheats: "$(xdg-user-dir DOWNLOAD)/vg"
