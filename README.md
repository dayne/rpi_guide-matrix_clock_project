# Guide: Raspberry Pi RGB Matrix Clock

A guide to building a Raspberry Pi LED Matrix Clock to be used by STEAM student and teachers participating or follow curriculum developed by the NSF grant Teaching Through Technology (T3), a project developed to support Science Technology Engineering Arts (STEAM). The goal of of T3 (insert formal project goal).  The Raspberry Pi Matrix Clock Project `rpi_guide-matrix_clock_project` was developed to support the T3 STEAM objectives by introducing a flexible platform, Raspberry Pi and an LED Matrix, to teach a variety of hardware, software, and network technologies to K-12 students and teachers.

The inspiration for this project was from the request by the [Hydaburg City School](http://www.hydaburg.k12.ak.us/) as part of the support of their 2017 STEAMFest. The school was in need of clocks through out their three campus buildings for students and teachers to reference and the T3 team used that need to put together this clock kit using a combination of custom hardware with off the shelf hardware and softwar.  The clock project allows students and teachers to work through building the hardware, configuring software, and integrating into their network a Raspberry Pi based LED Matrix clock with future expanstion capabilities of a PA system, scrolling messages, or wherever their imagination takes them.

See the [credits](#credits) section below for collaborators and contributors to this project. We welcome support and [contributions](#contributing) to this guide.

## Requirements

### Hardware requirements

* Raspberry Pi
* SD Card
* 4xLED Matrix & cables & screws
* Custom Raspberry Pi matrix hat
* 5V Power Supply with (?) amps

### Software requirements

To get the basic functionality of the clock the software requirements are extremely minimal:

* [Current version of Raspbian](https://www.raspberrypi.org/downloads/raspbian/)
  * _Raspbian Stretch 2017-11-29 at time of writing_
* [hzeller/rpi-rgb-led-matrix](https://github.com/hzeller/rpi-rgb-led-matrix/]
* Lttle bit of configuration for the local network pi is being deployed at.

## Setup

### Hardware setup

_Chester words here_

### Software setup

* Install latest Raspbian on SD card.
* Boot up with Pi connected to a monitor, keyboard and mouse
* Customize Raspbian 
 * Change `pi` password from the default of `raspbian`. 
   * _**Very important:** do this as we are about to enable ssh_
 * `sudo raspi-config`
   * set keyboard to US English
   * set timezone to local timezone
   * enable ssh
 * Give the pi a custom clock name
   * `sudo hostnamectl set-hostname 
 * Download and setup the (rpi-rgb matrix) software
 ```
   mkdir ~/projects
   cd ~/projects
   git clone https://github.com/hzeller/rpi-rgb-led-matrix.git
   cd rpi-rgb-led-matrix
   make
   cd examples-api-use
   make
   cd ../utils
   sudo apt install libgraphicsmagick++-dev libwebp-dev
   make
 ```
 
 At this point the Pi is is customized for your local timezone, network, and has the needed tools to talk to the LED matrix and is ready for network.
 
 ## disable sound
 
 Built in sound card for Raspberry Pi is not compatible with the matrix driver.  Best to disable it.
 
 Edit `/boot/config.txt` and find, towards the bottome of the file, the line:
 ```
 # Enable audio (loads snd_bcm2835)
dtparam=audio=on
```
and comment out the `dtparam` line like so:
```
# Enable audio (loads snd_bcm2835)
# dtparam=audio=on
```
 
 ## custom font
 
 Customize font size optimized for our click matrix (double the 9x18):
 
 ```
 sudo apt install bdfresize
 cd ~/rpi-rgb-led-matrix/fonts
 bdfresize -f 2 9x18.bdf > 18x36.bdf
 ```
 
 ## launching clock
 
 After making our custom 18x36.bdf font you can launch a full matrix clock like so:
```
cd ~projects/rpi-rgb-led-matrix/examples-api-use
sudo ./clock --led-chain=2 -f ../fonts/18x36.bdf
```
If that works you are ready to cause it to be launched on boot.

## launching on boot

You can add the clock launching command to `/etc/rc.local` so the clock.  You can edit it using `sudo nano /etc/rc.local/



By default it looks something like this on Raspbian.  
```
# By default this script does nothing.

# Print the IP address
_IP=$(hostname -I) || true
if [ "$_IP" ]; then
  printf "My IP address is %s\n" "$_IP"
fi

exit 0
```

Before the exit line we want to launch our clock by adding the following lines:
```
/home/pi/projects/rpi-rgb-led-matrix/examples-api-use/clock --led-chain=2 \
     -f /home/pi/projects/rpi-rgb-led-matrix/fonts/18x36.bdf \
     -d "%H:%M %p"
```

Upon a reboot you should be able to have clock launch on boot.

## Killing the clock after a boot

Say you added that line above to `/etc/rc.local` to launch the clock but you want to hack more and you'll need to kill the running clock command.

 
### Network Setup

_words written on airplane lost - need to rewrite them after I help somebody else go through this again_


### Clock on boot

_words written on plane lost :( - need to rewrite again_

# Next Steps

THe guide to this point has created clock using the demo tool provided as part of the [hzeller's](https://github.com/hzeller/)  [rpi-rgb-led-matrix](https://github.com/hzeller/rpi-rgb-led-matrix/) library.

This setup can be taken many directions at this point
* Setting up Node-Red to control the LED matrix and attach as an InternetOfThings targets
  * Streaming custom messages from various sources like twitter, email, or other services.
* Turning the Rpi into a network target for pixels streaming and use tools like [Processing](https://processing.org/) and the [rpi-matrix-pixelpusher]https://github.com/hzeller/rpi-matrix-pixelpusher) 

# Credits

This project was made possible through the collaboration and support of multiple existing projects and guides.

* NSF Project - Teaching Through Technology (TODO: award#)
* [Chester Lowrey](/clowrey) of [Easybiotics](http://www.easybotics.com) for developing the project and designing the custom hat to control the LED matrix.
* NFS Project - Modern Blanket Toss (TODO: award #)
* State of Alaska Title II-B MSP Grant to support Hydaburg and Hoonah's STEAM initatives.

## Contributing

We encourage contributions to this guide.  Pull requests are merged via Github, you can find the documentation about how to fork a repository and start contributing here [https://help.github.com/articles/fork-a-repo](https://help.github.com/articles/fork-a-repo).
