# WISSDOW PROJECT
> A 7/7 - 24/24 multi–live stream from the International Space Station ( ISS ).

![](GIF.gif)

## Table of Contents
- [Hardware ](#Hardware)
- [Installation](#installation)
- [Features](#features)
- [Known issues](#known-issues)
- [Help the project](#help)

## Hardware
> What you need before starting this project
- Single Board Computer
    - Used for this project : Raspberry Pi 2B
- Screen
    - Used for this project : Raspberry Pi Touchscreen Display 7″
- Case
    - Used for this project : SmartiPi Touch V1
- Power Cable
    - Used for this project : Raspberry Pi Universal Power Supply
- Speaker ( optional )

## Installation

> Easy to setup with a single board computer, takes about 6min to install. Brilliant !

### 1/3 Update your single board computer  

- In this example, I will use a Raspberry Pi running RaspbianOS.
```shell
$ sudo apt-get update
$ sudo apt-get upgrade
```

### 2/3 Download tools

- Streamlink
> We will use it to grab the multiples live streams.
```shell
$ sudo apt-get update
$ sudo apt install streamlink
```

- OMVXPLAYER
> Player used with STREAMLINK, preferred to VLC for the better personalization.
```shell
$ sudo apt-get update
$ sudo apt-get install omxplayer
```

- FBI
> We will use it to display our custom NASA loading page that will show up when the device is booting and switching cameras.
```shell
$ sudo apt-get update
$ sudo apt-get -y install fbi
```

### 3/3 Script

We are going to make a script that will launch during the boot of our single board computer. Put this pre-made one :
> For a Raspberry Pi, edit the **rc.local** script and put this script in :

```shell
#!/bin/bash

sudo fbi -T 1 --noverbose --fitwidth --autoup /home/pi/nasa.png
# Setting up the background “NASA” picture that will show up when the stream is either booting, or switching between the streams.

while true
# As it is always “TRUE”, the script will always try to start a stream, whatever happens.

do
streamlink --player omxplayer --fifo --player-args "--win \"0 0 800 480\" {filename}" https://www.youtube.com/watch?v=EEIk7gwjgIM 720p &
# First stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly.

sleep 18
# Wait few seconds before switching to the next stream.

pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch to the next stream” option with Livestreamer.

streamlink --player omxplayer --fifo --player-args "--orientation 180 --win \"0 0 800 480\" {filename}"  http://www.ustream.tv/channel/iss-hdev-payload best &
# Second stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly and the rotation for a better viewing experience.

sleep 18
# Wait few seconds before switching to the next stream.

pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch for next stream” option with Livestreamer.

streamlink --player omxplayer --fifo --player-args "--win \"0 0 800 480\" {filename}" http://www.ustream.tv/channel/live-iss-stream best &
# Third stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly.

sleep 18
# Wait few seconds before switching to the next stream.


pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch for next stream” option with Livestreamer.

done

```

---

## Features
 - Feature one
 
 - Feature two
 
 - Feature three

---

## Known Issues

- Sometimes, when a stream fail to display, the background show up until the “sleep” that is between streams is over. 

## Help

You can help the project by ...
