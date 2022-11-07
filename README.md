# ISS WINDOW PROJECT
> A 7/7 - 24/24 multi–live stream from the International Space Station ( ISS ).

![](GIF.gif)

## Table of Contents
- [Hardware ](#Hardware)
- [Installation](#installation)
- [Features](#features)
- [Upcoming Features](#upcoming-features)
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
Automatic install :
Run the ISSetup.sh script ( coming soon )

Manual install : 
> Easy to setup with a single board computer, takes about 6min to install manually. Brilliant !

### 1/3 Download tools

- Update your single board computer
> In this example, I will use a Raspberry Pi running RaspbianOS.
```shell
$ sudo apt-get update
$ sudo apt-get upgrade
```

- STREAMLINK
> We will use it to grab the multiples live streams.
```shell
$ sudo apt-get install streamlink
```

- OMVXPLAYER
> Player used with STREAMLINK, preferred to VLC for the better personalization.
```shell
$ sudo apt-get install omxplayer
```

- FBI
> We will use it to display our custom NASA loading page that will show up when the device is booting and switching cameras.
```shell
$ sudo apt-get -y install fbi
```
### 2/3 Setup the background

Download the background.png file.
> If you are running this project with a RaspberryPi, put the background in **/home/pi/**.

### 3/3 Boot-Script

We are going to make a script that will launch during the boot of our single board computer.
Create the script "iss-streamer" and put this code in your home directory :
> For a Raspberry Pi, put it in /home/pi

```shell
#!/bin/bash

sudo fbi -T 1 --noverbose --fitwidth --autoup /home/pi/nasa.png
# Setting up the background “NASA” picture that will show up when the stream is either booting, or switching between the streams.

while true
# As it is always “TRUE”, the script will always try to start a stream, whatever happens.

do
# First stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly.

streamlink --player omxplayer --fifo --player-args "--win \"0 0 800 480\" {filename}" https://www.youtube.com/watch?v=86YLFOog4GM&t=0s 720p &
sleep 150
# Wait few seconds before switching to the next stream.
pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch to the next stream” option with Livestreamer.

streamlink --player omxplayer --fifo --player-args "--orientation 180 --win \"0 0 800 480\" {filename}" http://www.ustream.tv/channel/iss-hdev-payload best &
# Second stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly and the rotation for a better viewing experience.
sleep 150
# Wait few seconds before switching to the next stream.
pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch to the next stream” option with Livestreamer.

streamlink --player omxplayer --fifo --player-args "--win \"0 0 800 480\" {filename}" http://www.ustream.tv/channel/live-iss-stream best &
# Third stream start with OMXPLAYER, and arguments that will make the player fit the screen size properly.
sleep 150
# Wait few seconds before switching to the next stream.
pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch to the next stream” option with Livestreamer.

streamlink --player omxplayer --fifo --player-args "--win \"0 0 800 480\" {filename}" https://www.youtube.com/watch?v=21X5lGlDOfg 720p &
sleep 150
# Wait few seconds before switching to the next stream.
pkill omxplayer
# Kill OMXPLAYER in order to start the next stream, as there is no proper “switch to the next stream” option with Livestreamer.

done

```

Now that the script is created, we are going to call it in the boot script
> For a Raspberry Pi, go to /etc and edit the **rc.local** script by putting this code in :

```shell

#!/bin/sh

# start the ISS video stream
bash /[PATH-TO-SCRIPT-FROM-ROOT]/scriptISS.sh
exit 0

```

**We are all set ! Reboot and enjoy your brand new virtual window!**

---

## Features
 - Plug and Play
 
 - No need to touch anything after a power outage
 
 - No command line visible even after a stream failure
 
 ## Upcoming Features
 
 - Automatic screen size detection !
 - Ability to listen to live conversations between Earth and the ISS astronauts !
 - Blinking leds when the ISS pass above your location !
 - Screen dimming !
 - Touch-to-wake !
 - Live 3D Tracker !
 - Multiple background style and size for a better fit with your screen !
 - More features coming soon...

---

## Known Issues

- When a stream fail to display, the background show up until the “sleep” (which is between the streams) is over. 

## Help

You can help the project by ...
