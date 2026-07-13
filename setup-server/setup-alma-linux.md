# Setting up Alma Linux

For this part of the install, see [also](https://linux.web.cern.ch/almalinux/alma9/stepbystep/).&#x20;

When the server has booted Alma Linux, you will now need to install it. Choose your boot drive in the menu in the top right.

Make sure that the ethernet cable is plugged into a numbered outlet on the wall, and in one of the outlets on the back of the server. The server has two outlets. You will either need to configure both of the outlets, or just remember which outlet the cable was plugged into, since access to the CERN servers is determined by the hardware address of the outlet on the server. Now go to internet connections and check the Hardware address, it will look something like: `10:C3:7B:20:62:89` You will need to add this to accepted computers on CERN, via this address: [https://landb.cern.ch/portal/devices/register](https://landb.cern.ch/portal/devices/register) Add the name in the top: `AliFoc-XX` where the x's are the next number in the server system, e.g. 05

On the right the server is a computer, and has server model, something. For the first added servers, it was an ASUS with serial no. ESC4000-FDR GS2 Add all additional information, and in the bottom, click on the +add symbol and write the Hardware address. Now it will begin the registration process, this will take a few minutes. After it is done, and the ethernet cable is connected you may go to the next step.

Go to installation source, and put in this address: [linuxsoft.cern.ch/cern/alma/9.5/CERN/x86\_64](https://linuxsoft.cern.ch/cern/alma/9.5/CERN/x86_64) It is important that this is the 9.5 and not just 9 or any other distro.

For the "On the network path", put Closest mirror and then the path listed above. Then add additional repository by clicking the `+` icon in the box, and putting `https://` in the dropdown box, and then the path listed above.

If this has been done correctly, choose the correct software:

For software selection, choose: In CERN tools, add CERN Base Tools and CERN Addons

In Server Development tools, legacy UNIX compatibility, System tools, Scientific support and more perhaps, this can be added later.

Add a server User and a server password, both of these could be anything, but remember to write them down, these will be crucial later.

Now there shouldn't be anymore flags, and you can press the button: <kbd>Begin install</kbd>, and you will now begin installing Alma Linux 9.5 on your server.

The configuration of the server, can now be done afterwards.

When rebooting the server after the installation, make sure to take the USB stick out.
