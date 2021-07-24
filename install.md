Thinkpad Setup
==============

    Config
        Keyboard/Mouse
            Fn and Ctrl Key swap Enabled
        Beep and Alarm
            Keyboard Beep Disabled
    Startup
        UEFI/Legacy Boot
            UEFI/Legacy Boot Priority
                UEFI First

Scripts
=======

    iwctl
    curl -sL https://raw.githubusercontent.com/ppsqkk/backup/main/scripts/1
    arch-chroot /mnt

    curl -sL https://raw.githubusercontent.com/ppsqkk/backup/main/scripts/2
    exit
    reboot

    # As root
    nmcli
    curl -sL https://raw.githubusercontent.com/ppsqkk/backup/main/scripts/3
    exit

    # As non-root
    curl -sL https://raw.githubusercontent.com/ppsqkk/backup/main/scripts/4
    exit

    rclone config
    # Get data backup
    curl -sL https://raw.githubusercontent.com/ppsqkk/backup/main/scripts/5
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
