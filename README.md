# rpi_guide-matrix_clock_project

A guide to building a Raspberry Pi LED Matrix Clock to be used by STEAM student and teachers participating or follow curriculum developed by the NSF grant Teaching Through Technology (T3), a project developed to support Science Technology Engineering Arts (STEAM). The goal of of T3 (insert formal project goal).  The Raspberry Pi Matrix Clock Project `rpi_guide-matrix_clock_project` was developed to support the T3 STEAM objectives by introducing a flexible platform, Raspberry Pi and an LED Matrix, to teach a variety of hardware, software, and network technologies to K-12 students and teachers.

The inspiration for this project was from the request by the [Hydaburg City School](http://www.hydaburg.k12.ak.us/) as part of the support of their 2017 STEAMFest. The school was in need of clocks through out their three campus buildings for students and teachers to reference and the T3 team used that need to put together this clock kit using a combination of custom hardware with off the shelf hardware and softwar.  The clock project allows students and teachers to work through building the hardware, configuring software, and integrating into their network a Raspberry Pi based LED Matrix clock with future expanstion capabilities of a PA system, scrolling messages, or wherever their imagination takes them.

See the [credits](#credits) section below for collaborators and contributors to this project.

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

(Chester draft words here)

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
   git clone (url)
   cd (repo)
   make
   cd (examples)
   make
   cd ../(utils)
   sudo apt-get install (stuff)
   make
 ```
 * 
 
 At this point the Pi is is customized for your local timezone, network, and has the needed tools to talk to the LED matrix and is ready for network.
 
### Network Setup

_words written on airplane lost - need to rewrite them after I help somebody else go through this again_

# Credits

This project was made possible through the collaboration and support of multiple existing projects and guides.

* NSF Project - Teaching Through Technology (TODO: award#)
* [Chester Lowrey](/clowrey) of [Easybiotics](http://www.easybotics.com) for developing the project and designing the custom hat to control the LED matrix.
* NFS Project - Modern Blanket Toss (TODO: award #)
* State of Alaska Title II-B MSP Grant to support Hydaburg and Hoonah's STEAM initatives.

