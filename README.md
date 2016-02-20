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

Headphones now work (a bit of noise on the line), but the desktop speakers do not. Forcing to HDMI does not seem to work, at least with those same speakers.

## Docker SD card image

Now to prep an SD card for the rpi2 that is geared to just doing docker stuff. I used this link:

http://blog.hypriot.com/getting-started-with-docker-and-mac-on-the-raspberry-pi/

Used hypriot-rpi-20151115-132854.img.zip.

I used a secondary SD card instead of the one that had the NOOBS image, just in case I wanted to get back to it later.

Placed the SD card and booted up, connected to HDMI display. Plugged in ethernet after boot.

During boot, saw messages about `cfg80211: Calling CRDA to update world regulatory domain`, followed a recommendation [here](https://github.com/raspberrypi/linux/issues/1149) to do:

`sudo apt-get install crda`

but this failed with some "Could not resolve 'mirrordirector.raspbian.org'" errors, so skipping that for now. Will be using docker for new images anyway.

For wifi, had to create wpa_supplicant.conf and set it up with the network info.

Did a `apt-get install make` since the speakerbot project uses a make file.

## Docker stuff

See speakerbot repo. Once got a Dockerfile set up:

```
docker build -t speakerbot .

docker run -it speakerbot
```


## Unix commands

For shutdown: `sudo poweroff`
For restart: `sudo reboot`

