## Table of Contents
- [Installation](#installation)
- [Features](#features)
- [Known issues](#known-issues)
- [Help the project](#help)

![](GIF.gif)

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
```shell
$ sudo apt-get update
$ sudo apt install streamlink
```

- OMVXPLAYER
```shell
$ sudo apt-get update
$ sudo apt-get install omxplayer
```

- FBI
```shell
$ sudo apt-get update
$ sudo apt-get -y install fbi
```
--

### 3/3 Script

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

- First Issue
- Second Issue

## Help

You can help the project by ...
