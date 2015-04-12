---
layout: post
category : arch
title : Arch Linux- Do it yourself
tagline: ""
tags : [Linux, Arch]
---

>The Linux philosophy is 'Laugh in the face of danger'. Oops. Wrong One. 'Do it yourself'. Yes, that's it! -Linus Torvalds

Arch Linux! I will give the reasons why should one choose Arch Linux over an other distro. Installing Arch Linux is pretty difficult task when you atempt to do it for your first time if you are not familiar with command line and basics of linux. But I would suggest you to install Arch Linux as you will gain a very good insight on how linux works. Arch linux is a minimal, [bleeding-edge](https://www.archlinux.org/about/) distro and you won't have unnecessary packages/drivers or whatever preinstalled. You shape your OS as it suits your needs. Let's get started!

##Before getting started
Make sure you've downloaded the arch dual_iso (Arch ISO is dual arch meaning you can install either 32 bit or 64 bit version of Arch using the same media) from [here](http://mirror.cse.iitk.ac.in/archlinux/iso/) and dd it. If you got no idea what dd is, arch ain't for you friend! Please be sure you are connected to wifi or plug-in an ethernet cable. If you've got UEFI motheboard, the procedure is pretty same but you gotta do some tweaks with grub, which I will explain later, as I experienced the UEFI pain.

##./arch

###Step 1 : Partitioning
Boot your iso and choose your architecture.

    lsblk
This will get you the list of previously made partitions. Let us start partitioning.

    cgdisk /dev/sda
 Hover to the partition where we gotta install arch and use right/left arrow keys to delete it. You should see the free space left and here we will be installing arch.

#####Boot Partition

BIOS-GPT requires BIOS Boot Partition at the beginning of the disk. The Free Space is already selected then

    Hit New -> Enter
    First Sector -> Enter
    Size in Sector -> 1007KiB -> Enter
    Hex Code of GUID (L to show codes, Enter = 8300) -> ef02 ->Enter
    Enter partition name – > Enter

You will notice a 1007.0 KiB BIOS boot partition has been created.

####Create root

Use keyboard to select the free space

    Hit New -> Enter
    First Sector -> Enter
    Now it will ask you how much space you want to allocate to that partition. In my case I will give root over 40GB
    Size in Sector -> 40GB -> Enter
    Hex Code of GUID (L to show codes, Enter = 8300) -> Enter
    Enter partition name – > Enter

I've got a 500GB hard drive and chose root partition to be 40GB. Choose accordingly.

####Creating Swap

If you use suspend/hibernate, you need swap. Depending on your need, you can create swap. Let it be same as the size of your RAM. Use keyboard and select Free Space

    Hit New -> Enter
    First Sector -> Enter
    Now it will ask you how much space you want to allocate to that partition. I would give 4GB for swap (check what’s recommended)
    Size in Sector -> 4GB -> Enter
    Hex Code of GUID (L to show codes, Enter = 8300) -> Enter
    Enter partition name – > swap

Swap has been created.

####Creating Home

Let the rest of the space be alloted to home. Use keyboard and select Free Space

    Hit New -> Enter
    First Sector -> Enter
    Now it will ask you how much space you want to allocate to that partition. Here I am giving the remaining space to home.
    Size in Sector -> 200GB -> Enter
    Hex Code of GUID (L to show codes, Enter = 8300) -> Enter
    Enter partition name – > home -> Enter

If everything looks good select ‘Write‘, which will ask you to confirm if you want to write the changes. Type ‘yes‘ if you are sure. Once done select ‘Quit‘.

Lastly, check

    fdisk -l
This will get you the info of your current partition layout.

###Step 2 : Creating Filesystem

In my case, the partitions were

    sda1 – BIOS Boot
    sda2 – root
    sda3 – swap
    sda4 – home

We will format'em all with ext4 file system

    mkfs.ext4 /dev/sda2
    mkfs.ext4 /dev/sda4

Formatting Swap,

    mkswap /dev/sda3
    swapon /dev/sda3

>Make sure you select appropriate partitions instead of sda3

Check it again,

    lsblk /dev/sda

###Step 3 : Mounting

Mount the root partition and then create home directory.

    mount /dev/sda2 /mnt

Create and mount home directory

    mkdir /mnt/home
    mount /dev/sda4 /mnt/home

###Step 4 : Installing base

Let us install base packages for the system. Make sure about your internet connection by running

    wifi-menu

and select your access point. And then,

    pacstrap -i /mnt base base-devel

###Step 5 : Creating fstab

    genfstab -U -p /mnt >> /mnt/etc/fstab

>Run the above command only once even if there are any issues.

In case of any errors, configure it manually 

    nano /mnt/etc/fstab

Let us chroot into the system

    arch-chroot /mnt

###Step 6 : Setting up language, location and timezone

Choose the language that you use. To set the language, run the following command:

    nano /etc/locale.gen

By default every entry in locale.gen file is commented out and we need to uncomment the languages we want. Uncomment,

>en_US.UTF-8 UTF-8

Ctrl-X and type Y to save and exit

Run,

    locale-gen
    echo LANG=en_US.UTF-8 > /etc/locale.conf
    export LANG=en_US.UTF-8

Let us setup the timezone

    ls /usr/share/zoneinfo/

  will list you the timezones. Mine is Asia/Kolkata

    ls /usr/share/zoneinfo/Asia

Then, run

    ln -s /usr/share/zoneinfo/Asia/Kolkata /etc/localtime

###Step 7 : Configuring hardware clock and network

If you are planning to use only linux, run this

    hwclock --systohc --utc

If alongside with windows, run this

    hwclock --systohc --localtime

In case you are connected to wifi, install the wifi tools and enable wireless service

     pacman -S wireless_tools wpa_supplicant wpa_actiond dialog
     wifi-menu
     systemctl enable net-auto-wireless.service

In-case of ethernet,

    systemctl enable dhcpcd@eth0.service

###Step 8 : Setting-up accounts

Create root password,

    passwd

And add user

    useradd -m -g users -G wheel -s /bin/bash dolftax

>Replace dolftax by your username

Password for you,

    passwd dolftax

Umm! Installing and configuring sudo, by

    pacman -S sudo
    EDITOR=nano visudo

and uncomment

    %wheel ALL=(ALL) ALL

Ctrl-X and type Y to save and exit

###Step 9 : Time for grub

Install grub2 by following command and don't forget to replace 'sda' with your relevant hard disk. If you've got UEFI motherboard, disable it while booting up. It should work, if not configure your bootloader [here](https://wiki.archlinux.org/index.php/beginners%27_guide##For_UEFI_motherboards)

    pacman -S grub-bios
    grub-install --target=i386-pc --recheck /dev/sda
    cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

Install os-prober and configure grub

    pacman -S os-prober
    grub-mkconfig -o /boot/grub/grub.cfg

Now if you have installed 64 bit Arch we need to add the multilib repo to pacman's repo list. Here's how you do it

    nano /etc/pacman.conf

Go to "Repositories" section of the configuration file and add the following at the bottom

    [multilib]
    Include = /etc/pacman.d/mirrorlist

Ctrl+X, and they Y to save and exit.It's time to exit from the chroot

    exit

Unmount the root partition 

    umount /mnt 

And reboot

    reboot

###Step 10 : Installing X and drivers

Let the X server be installed,

    pacman -S xorg-server xorg-server-utils xorg-xinit

And mesa for 3D-support

    pacman -S mesa

Install appropriate video driver by following the instructions [here](https://wiki.archlinux.org/index.php/X_server##Driver_installation). 

Install Synaptics driver, (in case of laptop)

    pacman -S xf86-input-synaptics

Let us set-up the default environment,

    pacman -S xorg-twm xorg-xclock xterm

And

    startx

If everything went perfect, x window will be displayed. Yay! Type, exit.

###Step 11 : Installing Desktop Environment

I would prefer xfce. Install the following packages

    sudo pacman -S xfce4 xfce4-goodies alsa-utils pulseaudio dbus slim

Install the correct driver for your graphics card. These are the likely options

* xf86-video-ati
* xf86-video-nv
* xf86-video-intel
Run,

    pacman -S xf86-video-intel

>Replace intel with the options mentioned above, according to your graphics card

Ennable NetworkManager

    systemctl enable NetworkManager

Let us configure [Slim](https://wiki.archlinux.org/index.php/SLiM) which is a login manager.

    cp /etc/skel/.xinitrc ~/.xinitrc
    cp /etc/skel/.xsession ~/.xsession

And then, run

    sudo nano ~/.xinitrc

Uncomment the line

    ## exec startxfce4

So that it looks like,

    exec startxfce4

Restart the slim service

    systemctl enable slim.service

###YEEEHAH! You made it!###

If you face any error, '[duck duck go](http://duckduckgo.com)' it, even if you couldn't resolve, comment below!

####Extras

#####Installing packages from AUR

If a package couldn't be found by pacman, you can install it from [AUR (Arch User Repository)](https://aur.archlinux.org/) . Guidelines to install packages from AUR is [here](https://wiki.archlinux.org/index.php/AUR_User_Guidelines##Installing_packages). Aura, another multilingual package manager would build and install the package for you. Find more about Aura here - [https://wiki.archlinux.org/index.php/Aura](https://wiki.archlinux.org/index.php/Aura). You can now search for packages from AUR by

    sudo aura -A 'package_name'

as this would resolve all the dependencies, make the package and install it.

#####Network Manager issues

In case of any network manager error, go [here](https://wiki.archlinux.org/index.php/NetworkManager) . To get list of networks and connect to them through terminal, you could run

    sudo wifi-menu

Update: Ater publishing this post, a vivid discussion took place on Hacker News - https://news.ycombinator.com/item?id=9332978

Cheers!
