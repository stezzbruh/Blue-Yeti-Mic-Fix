# Blue-Yeti-Mic-Fixe
fix for blue yeti mic not loading on boot
step 1: place alsa-base.conf into /etc/modprobe.d after deleting the old one if there is a alsa-base.conf unlready sitting there
step 2: place default.pa and system.pa into /etc/pulse after deleting the old versions of default.pa and system.pa
step 3: reboot 
