Start by downloading the image of Alma Linux 9.5 onto your pc, by following this link: https://linuxsoft.cern.ch/cern/alma/9.5/BaseOS/x86_64/os/images/boot.iso
The image will take up 1 GB of storage. 
Then reformat your USB drive and put the image onto the USB stick. 

Before plugging anything in, make sure that at there's an ssd in the first slot (the one most to the left) in the server, and no other disks.
The server will sometimes fail to boot if two drives is in the server at the same time while trying to configure a new bootdrive, due to them being connected by a former RAID configuration.

Then, plug everything in, and turn on the server. 
The powerbutton is on the front right side of the server as well as an extra button which also needs to be on. 

Now plug everything on and press the two buttons. 
If the server is plugged in correctly and the buttons have been pressed, the two green lights above the powercable, as well as the light above the powerbutton and the ethernet cable should be green. If the lights above the powercables are yellow, the powerbutton has not been pressed. 
The second light underneath the powerbutton should be blue. 

The server will now try booting. By pressing repeatedly on delete, whilst the server is booting you can access the BIOS. 
First, go to "Advanced" and then PCH SATA configuration. from here you will change the configuration from RAID to AHCI, all other settings that will now appear, should not be changed. 
Now go to the "boot" menu, and enter "CSM Parameters". From here you will need to make sure that all the settings are Legacy.
Exit CSM Parameters and go to the boot menu, make sure that the server is booting from your USB drive. 
Press f10 then yes to save and exit. 

If done correctly the server will now ask you if you want to install Alma Linux or try and then install Alma Linux. 
Choose try and then install.
