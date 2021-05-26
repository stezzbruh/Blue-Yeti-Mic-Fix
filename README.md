# Blue-Yeti-Mic-Fix
fix for blue yeti mic not loading on boot
(warning may need to change some values if you a 3.5mm jack headset)


step 1: 
go to ``/etc/modprobe.d`` and move the old ``alsa-base.conf`` to another location like Documents

step 2:
place ``alsa-base.conf`` into ``/etc/modprobe.d`` after moving the old one if there is a ``alsa-base.conf`` sitting in ``/etc/modprobe.d`` (some distros don't have one be default)

step 3: edit and replace (or even just delete) these in the new ``alsa-base.conf`` you got from me with your own 

options bt87x index=-2

options cx88_alsa index=-2

options saa7134-alsa index=-2

options snd-atiixp-modem index=-2

options snd-intel8x0m index=-2

options snd-via82xx-modem index=-2

options snd-usb-caiaq index=-2

options snd-usb-ua101 index=-2

options snd-usb-us122l index=-2

options snd-usb-usx2y index=-2

use this references: 
https://askubuntu.com/questions/1230016/headset-microphone-not-working-on-ubuntu-20-04

``Use cat /proc/asound/card*/codec* | grep Codec to get the Audio Codec for your machine model. In my case I saw Audio (ex: Codec: Realtek ALC233) & Video (ex: Codec: Nvidia GPU 94 HDMI/DP) codecs there.``

``Go to www.kernel.org and look up the version of the codec, and get the full name of it. In my case: Realtek ALC233 -> alc233-eapd.``

``Create/update a file under /etc/modprobe.d/alsa-base.conf, and add this line: options snd-hda-intel model=alc233-eapd, while replacing model with your own.``

step 4: 
place ``default.pa`` and ``system.pa`` into ``/etc/pulse`` after deleting the old versions of ``default.pa`` and ``system.pa`` in ``/etc/pulse``




optional step: 
open terminal and type ``pacmd list-sources`` then go into ``default.pa`` and change ``set-default-source input`` to your prefered device ``set-default-source name-of-driver`` for example my blue yeti it is called alsa_card.usb-Generic_Blue_Microphones_2036BAB0DFR8-00



final step: 
``sudo reboot``
