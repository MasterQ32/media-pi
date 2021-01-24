# MediaPi

This repo contains configuration files to create a small standalone multimedia node that can play/stream music via:
- Bluetooth A2DP
- ZeroConf PulseAudio streaming

## Installation Instruction

Clone this repo into the default user `/home/alarm/media-pi`. Copy everything from `etc` into `/etc`

### Command sequence

Run as root:
```

git clone https://github.com/MasterQ32/media-pi

cp -r media-pi/etc /etc

useradd --home-dir /var/run/pulse pulse
gpasswd -a pulse audio

pacman -Syu alsa-firmware alsa-lib alsa-utils avahi pulseaudio pulseaudio-zeroconf bluez python-dbus python-gobject pulseaudio-bluetooth brcm-patchram-plus

echo "dtparam=audio=on" >> /boot/config.txt
echo "audio_pwm_mode=2" >> /boot/config.txt

systemctl --global disable pulseaudio.service pulseaudio.socket

systemctl enable avahi-daemon
systemctl enable pulseaudio
systemctl enable bluetooth
systemctl enable bluetooth-agent
systemctl enable bluetooth-driver
```

## Further Reading

- https://scribles.net/auto-power-on-bluetooth-adapter-on-boot-up/
- https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/
- https://hwblog.org/2018/06/08/how-to-get-bluetooth-working-on-raspberry-pi-3-model-b-or-b-with-arch-linux-arm/
- https://github.com/RPi-Distro/bluez-firmware/tree/master/broadcom (firmware bin)
- https://github.com/pauloborges/bluez/blob/master/lib/uuid.h


