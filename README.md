# XR18RecRaspi4

Headless multitrack audio recording for Behringer XR18 on Raspberry Pi 4.

This is a fork from **capPiture**. Please consider using the original project [capPiture](https://github.com/danielappelt/capPiture). Mainly changes are:

- Use of *gpiodetect*, *gpioget*, *gpioset* instead of *echo in*
- Use of a usb drive instead of the sd card for storing the recordings
- Use ssh (not necesary, but useful)

# Installation

First install **Raspberry Pi OS Lite** on Raspberry 4 with the Raspberry Pi Imager with the following settings(See this instructions for more details: https://www.raspberrypi.com/software/operating-systems):

- Set locale
- Akcivate ssh
- Set hostname (e.g. to xr18rec)

Then copy the bin folder to */home/pi* of the raspberry pi sd card

Then start the Raspberry Pi with this card and:

- Connect to the raspberry pi via ssh
- Run these commands :

```bash
sudo apt update
sudo apt ugrade
sudo apt install --no-install-recommends jackd2 jack-capture dbus-x11
echo "startcapiture" >> /home/pi/.profile
sudo mkdir /mnt/usb
sudo chown pi:pi /mnt/usb
```

Run **sudo raspi-config** and enable auto login

Restart the raspberry pi
## GPIO

- Connect *GPIO26* to the + leg of an LED with a 330 Ohm resistor in between, other leg to gnd
- Attach buttons to *GPI19* and *GPI13*. *GPI19* starts and stops recording, *GPI13* deletes the last recording. *GPI19* + *GPI13* powers off the Rpi.
- LED light codes:
    - **Off:** no connection to XR18
    - **blinking (0.5 seconds intervall) + 2 seconds off:** no connection to USB stick
    - **On:** recording can start
    - **blinking (1 second intervall):** recording is in progress



## TODO:
- improve usb drive detection (now only works for sda1 dev).
