# Linux

This part of the repo documents my linux setup and usage

Currently using:

- Debian 12 with xfce on ThinkPad X230

---

## The process

1. Create a bootable USB from my Macbook Air

    - [Resource](https://umatechnology.org/how-to-create-and-boot-from-a-linux-usb-drive-on-mac/)
    
       -  **It turns out there's no need to worry about "GUID Partition Map" as long as it's set to "MS-DOS (FAT)" as the format.**
       - `diskutil` is a handy tool from mac that you can use to unmount, eject and list out the drives in your system

       - `dd` another handy tool that comes from mac that allows you to write the iso image to the usb

       - Recommended usage for `dd`: `sudo dd if=linux.img.dmg of=/dev/diskN bs=1m status=progress` 

2. Install the linux on the laptop

    - mount the usb first

    - press f12 on boot

    - follow the graphical installation guide

3. Things can go wrong after installation (for Debian)

    - `apt install` won't work because you're not one of the sudoers

        - the fix: `sudo usermod -aG sudo [username]`

    - `apt install` works but throw the cdrom error

        - [Resource](https://my.velocihost.net/knowledgebase/29/Fix-the-apt-get-install-error-Media-change-please-insert-the-disc-labeled--on-your-Linux-VPS.html)

        - comment out something like: deb cdrom:[Debian GNU/Linux 7.0.0 _Wheezy_ - Official amd64 CD Binary-1 20130504-14:44]/ wheezy main in sources.list file
        
4. Set up Firewall using ufw

    - `apt install ufw` install user friendly firewall
    - `sudo ufw allow ssh` to allow ssh for things like github
    - `sudo ufw status` check status
5. Speed up the boot time

    - `sudo vi /etc/default/grub` update the grub file
    - set `GRUB_TIMEOUT=0`; then save and exit
    - `sudo update-grub` update grub