# Blue-Yeti-Mic-Fix (Ubuntu and Ubuntu-based)
fix for blue yeti mic not loading on boot
(warning may need to change some values if you a 3.5mm jack headset)


step 1: 
go to ``/etc/modprobe.d`` and move the old ``alsa-base.conf`` to another location like Documents

step 2:
place ``alsa-base.conf`` into ``/etc/modprobe.d`` after moving the old one if there is a ``alsa-base.conf`` sitting in ``/etc/modprobe.d`` (some distros don't have one be default)

step 3: edit and replace (or even just delete) these in the new ``alsa-base.conf`` you got from me with your own ``sudo nano /etc/modprobe.d/alsa-base.conf``

``options bt87x index=-2

options cx88_alsa index=-2

options saa7134-alsa index=-2

options snd-atiixp-modem index=-2

options snd-intel8x0m index=-2

options snd-via82xx-modem index=-2

options snd-usb-caiaq index=-2

options snd-usb-ua101 index=-2

options snd-usb-us122l index=-2

options snd-usb-usx2y index=-2``

use this reference: 
https://askubuntu.com/questions/1230016/headset-microphone-not-working-on-ubuntu-20-04

``Use cat /proc/asound/card*/codec* | grep Codec to get the Audio Codec for your machine model. In my case I saw Audio (ex: Codec: Realtek ALC233) & Video (ex: Codec: Nvidia GPU 94 HDMI/DP) codecs there.``

``Go to www.kernel.org and look up the version of the codec, and get the full name of it. In my case: Realtek ALC233 -> alc233-eapd.``

``Create/update a file under /etc/modprobe.d/alsa-base.conf, and add this line: options snd-hda-intel index=1, while replacing model with your own.``

use this reference: https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture

``Configuring the index order via kernel module options``

``If your sound card order changes on boot, you can specify their order in any file ending with .conf in /etc/modprobe.d (/etc/modprobe.d/alsa-base.conf is suggested). For example, if you want your mia sound card to be #0:``

``/etc/modprobe.d/alsa-base.conf

options snd_mia index=0

options snd_hda_intel index=1``

``Use $ cat /proc/asound/modules to get the loaded sound modules and their order. This list is usually all that is needed for the loading order. Use $ lsmod | grep snd to get a devices & modules list. This configuration assumes you have one mia sound card using snd_mia and one (e.g. onboard) card using snd_hda_intel.``

``You can also provide an index of -2 to instruct ALSA to never use a card as the primary one. Distributions such as Linux Mint and Ubuntu use the following settings to avoid USB and other "abnormal" drivers from getting index 0``

step 4: 
place ``default.pa`` and ``system.pa`` into ``/etc/pulse`` after deleting the old versions of ``default.pa`` and ``system.pa`` in ``/etc/pulse``




optional step (for people with a 3.5mm jack headset plugged into PC directly): 
open 2 terminals and type ``pacmd list-sources`` in 1 then go do ``sudo nano /etc/modprob.d/default.pa`` in the other and change ``#set-default-source input`` to your prefered device ``set-default-source name-of-driver`` 

for example my blue yeti it is called alsa_card.usb-Generic_Blue_Microphones_2036BAB0DFR8-00 so it looks like 
``set-default-source alsa_card.usb-Generic_Blue_Microphones_2036BAB0DFR8-00``


final step: 
``sudo reboot``

and if even that doesn't work. this last bit should do the trick. just give it a second after rebooting it is a bit janky.
incomment the ``#`` on this line and add your blue yeti mic like the example below in ``/etc/pulse/default.pa``



```### Load audio drivers statically
### (it's probably better to not load these drivers manually, but instead
### use module-udev-detect -- see below -- for doing this automatically)
#load-module module-alsa-sink
load-module module-alsa-source device=hw:1,0 alsa_card.usb-Generic_Blue_Microphones_2036BAB0DFR8-00
#load-module module-oss device="/dev/dsp" sink_name=output source_name=input
#load-module module-oss-mmap device="/dev/dsp" sink_name=output source_name=input
#load-module module-null-sink
#load-module module-pipe-sink```
