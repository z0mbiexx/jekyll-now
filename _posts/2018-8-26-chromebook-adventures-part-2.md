---
layout: post
title: Adventures of the Chromebook Part 2 
---

So for anyone who actually read the first email i sent out they'd remember
i removed the write protection screw from the Asus C200 that Rex gave me..
and then i proceeded to unlock the developer edition of the chromeOS and
then i used https://mrchromebox.tech/#fwscript ;(Firmware Utility Script) to
overwrite the default BIOS of the chromebook with a custom EFI bios and
then i attempted to install Antergos and had it fail to a EFI issue so i
went with the Default Linux Distro for Chromebooks GalliumOS 2.1 for a
while.. and then went to the Alpha Branch of 3.0 for a bit. but i was never
really to happy since i prefer an Arch distro.. so this is where part two
comes into play..

i wiped the drive again and installed Antergos from an USB and again was
hit by the efi issue so it wouldn't boot.. well i found out by hitting
"ESC" while the bios loaded i could go into the Boot Maintenance Manager of
the BIOS and find the efi file by default from antergos and finally get my
chromebook to load antergos. but i obviously was not going to do this every
time.. so here comes the fix for the first issue with using an distro that
does not place the EFI in the right place when using a EFI based BIOS on a
chromebook

```
sudo su
mkdir -p /boot/efi/EFI/BOOT cp /boot/efi/EFI/antergos_grub/grubx64.efi
/boot/efi/EFI/BOOT/BOOTX64.efi
```

this fixed my issue with the distro not loading correctly on boot. so i now
had a working laptop without any "major" issues.. another issue with
chromebooks is the fact GalliumOS uses a custom kernel to have audio
working.. so i attempted to use the AUR (Arch User Repository) to build and
install the GalliumOS kernel for me and be done with it.. seemed easy and
was going to take no hassle. well unfortunately that meant it wanted to
sync that github on my laptop and then build the kernel from the machine
and then install it... issues with that was my chromebook only has 13gb of
storage.. so that solution instantly got shut down... so after a few hours
of googling and searching i finally found something on the
bugs.archlinux.org  for an older bug report with kernel 4.5.0.1 breaking
audio on these chromebooks.. and someone had a fix for it that worked for
them..  i tried it.. and i got it to work finally after many tries and
hours...

```
git clone --depth 1 https://github.com/plbossart/UCM.git
<https://github.com/plbossart/UCM.git>*
*cd UCM*
*sudo cp -r chtmax98090/ /usr/share/alsa/ucm/*
*alsaucm -c chtmax98090 set _verb HiFi set _enadev Speakers*
*sudo alsactl store*
```

running this initially would do nothing but throw up some errors about
parsing a certain file/folder and would never completely work so i gave up
for a bit.. and went back to googling and trying to find another solution..
and after finding no other working solution i tried again.. but this time..
i decided to look for the said folder and file on the machine to see what
was going on with those and why it wouldn't work.. and this is where i
finally found my solution to get working audio on my chromebook with kernel
4.18.4 and finally having it show the actual sound card rather then dummy
output..

```
i made the folder
/usr/share/alsa/ucm/GOOGLE-Quawks-1.0-Quawks/
and then i copied the files from
/usr/share/alsa/ucm/chtmax98090 to the newly created folder and then
renamed chtmax98090.conf to GOOGLE-Quawks-1.0-Quawks.conf
```

and reran the last two lines of the last commands i did before.. and rather
than having it spit errors out at me this time.. it worked and after a
reboot i had a working Chromebook with Arch and sound.. i do use Volume
Amplification because sound is a bit quiet to me.. but it at least works..
also with running Arch versus GalliumOS the trackpad on the Chromebook now
works as a normal laptop. no longer do i need to two finger tap the
trackpad for a right click it now somehow separated the bottom of the
trackpad for right click and left click.

i write this because Rex thought it would be a nice thing to allow others
to see the process and the ability of a chromebook with some tinkering and
a lot of bug fixing.
