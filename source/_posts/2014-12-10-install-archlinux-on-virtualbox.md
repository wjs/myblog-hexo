---
layout: post
title: virtualbox 上安装 archlinux
categories: [linux]
tags: [arch, linux]
---

早就想折腾一下arch，之前也试着在vmware和virtualbox里面安装过，可是人笨没办法，按照 [archwiki](https://wiki.archlinux.org/) 上的教程一步步走下来还是没装成功。昨晚再youtu上看到一个视频教程挺详细的，于是又折腾了一番，总算成功装上了。可以直接翻墙去看那个视频教程[Arch Linux VirtualBox Install (May 2013)](https://www.youtube.com/watch?v=8XLIw7Skq04)。这里记录一下 archwiki 上没有说清楚的一些步骤。  

跟着 archwiki 上的新手安装教程，走到 `arch-chroot /mnt` 这一步之后，就跟着下面的操作吧。


    arch-chroot /mnt 
    ls
    passwd
    nano /etc/locale.gen
    locale-gen
    ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    date
    echo arch > /etc/hostname
    nano /etc/hosts

    pacman -S grub-bios
    grub-install /dev/sda   # 就是 sda
    mkinitcpio -p linux
    grub-mkconfig -o /boot/grub/grub.cfg

    exit
    umount /mnt/home
    umount /mnt
    reboot


    ping www.baidu.com
    dhcpcd
    systemctl enable dhcpcd
    shutdown -P -h now


    nano /etc/pacman.conf
    # 去掉 [multilib] 和 它下面一行 的注释 （去掉这两行的注释）

    pacman -Syy
    pacman -Su

    pacman -S mlocate
    updatedb
    pacman -S alsa-utils
    alsamixer
    speaker-test -c2

    pacman -S xorg-server xorg-server-utils xorg-xinit 

    pacman -S virtualbox-guest-utils
    modprobe -a vboxguest vboxsf vboxvideo

    nano /etc/modules-load.d/virtualbox.config
    # 写入 #
    vboxguest
    vboxsf
    vboxvideo

    pacman -S xorg-twm xorg-xclock xterm

    startx
    exit


    EDITOR=nano visudo
    # 去掉 %wheel ALL=(ALL) ALL 那一行的注释

    useradd -m -g users -G storage,power,wheel -s /bin/bash wjs
    passwd wjs



    sudo pacman -S xfce4
    clear
    ls -la
    nano .xinitrc
    # 去掉 xfce 那一项的注释
    chmod +x .xinitrc
    ls -la
    clear

    sudo pacman -S xfce4-goodies

    startx