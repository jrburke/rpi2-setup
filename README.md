# Raspberry Pi 2 setup

Some scratch notes on setting up the rpi2 for some docker-based experiments.

I got the one with an SD Card already flashed with the NOOBS software, so starting it up was pretty easy.

Make sure the power supply is 5V 2A. I happened to have an old Samsung one for some other device laying around, so I used that with the micro usb cable.

Started off with wired ethernet connection, did a `sudo apt-get update` and `sudo apt-get upgrade` for the raspbian OS that came on the card.

## WIFI

Used a Tenda W311MI Wireless USB Adapter. After inserting it (and removing ethernet), then I used lsusb to confirm the device was visible.

Then in `/etc/wpa_supplicant/wpa_supplicant.conf`, added this to the bottom of the file:

```
network={
  ssid="YOUR_NETWORK_SSID"
  psk="YOUR_NETWORK_PASSWORD"
}
```

Then: `sudo ifdown wlan0 && sudo ifup wlan0`

These steps were found via [this blog post](http://www.jeffgeerling.com/blogs/jeff-geerling/edimax-ew-7811un-tenda-w311mi-wifi-raspberry-pi).

## Sound

I eventually want to use speakers connected to audio out to play sound, try a text to speech experiment.

* [Switched to the audio out instead of HDMI](https://www.raspberrypi.org/documentation/configuration/audio-config.md)

However, I don't hear sound. It sounds like the speaker are trying to make a noise, but something does not come out. TODO

