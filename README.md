# Blue-Yeti-Mic-Fix
fix for blue yeti mic not loading on boot



step 1: 
place ``alsa-base.conf`` into ``/etc/modprobe.d`` after deleting the old one if there is a ``alsa-base.conf`` sitting in ``/etc/modprobe.d`` (some distros don't have one be default)



step 2: 
place ``default.pa`` and ``system.pa`` into ``/etc/pulse`` after deleting the old versions of ``default.pa`` and ``system.pa`` in ``/etc/pulse``




optional step: 
open terminal and type ``pacmd list-sources`` then go into ``default.pa`` and change ``set-default-source input`` to your prefered device ``set-default-source name-of-driver`` for example my blue yeti it is called alsa_card.usb-Generic_Blue_Microphones_2036BAB0DFR8-00



final step: 
``sudo reboot``
