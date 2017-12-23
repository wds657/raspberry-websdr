# WebSDR node based on a Raspberry PI

### Requirements
- Raspberry PI 3
- Raspbian 9 installed and working
- Internet access setup and working
- RTL-SDR USB Dongle

### Required setup and software
```
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install g++ make libsigc++-1.2-dev libgsm1-dev libpopt-dev tcl8.5-dev libgcrypt-dev libspeex-dev libasound2-dev alsa-utils libqt4-dev
sudo apt-get install libsigc++ cmake groff rtl-sdr
```

### GPIO Setup
- Copy the etc/rc.local file to your /etc/rc.local
```
sudo cp etc/rc.local /etc/rc.local
```
- Check and match GPIO ports for relay control to switch antennas and a button to soft reset the Raspberry pi.


### Software reset
- There is a Python script that handles Raspberry PI reboots from a hardware switch without killing power.
- Check the /etc/rc.local file and match the desired GPIO port for this task.
- Copy lib/systemd/system/reset.service to /lib/systemd/system/reset.service
```
sudo cp opt/reset.py /opt/reset.py
sudo cp lib/systemd/system/reset.service to /lib/systemd/system/reset.service
chmod 644 /lib/systemd/system/reset.service
systemctl enable reset.service
systemctl start reset.service
```

### WebSDR
- Ask [Pieter](http://websdr.org/) to get a copy of WebSDR.
- Copy the websdr-rpi binary and files to your home directory (/home/pi/)
- Edit websdr-80m.cfg and websdr-40m.cfg to fulfill your configuration

### Cron
- I built a crontab configuration to switch between 40m and 80m bands time-based. Just import the crontab lines into your crontab.