![image](https://github.com/user-attachments/assets/f11f5d3a-4bc3-4ead-ba16-23fee96c62ab)
# Automated Remote Observatory Control &amp; Guard

ARO-Master is a project to implement an affordable and easy to build remote control system for Automated Remote/Robotic Observatories.
It's composed of two components:

### ARO-Master control box:
Hardware & firmware that implement the server/daemon for Observatory control (remote and local). This is the main brains that allows you to connect and control all the equipment, open/close the roof, see weather conditions, see the sky, see the observatory interior, control user login, control the Piers etc.
### Pier-Relays box:
Relays box for each pier that connected to ARO-Master, allows you to turn on and off the equipment (mount, PC, power box, etc.) 

## License:
When I made the decision to share this project I intended to make it public, but recent developments have changed that intention. So, for now I will share the firmware only in its compiled form (without the sources) and the hardware schematics are provided as reference material only.
There will be a commercial version that can be purchased as a kit or already assembled, in addition to the two electronic components mentioned (***ARO-Master box*** & ***Pier-Relays box***) there is also extra hardware that can be purchased by end users, such as the rack and pinion and motor for ceiling movement.

## Overview:
I started this project in 2015 and to date it has undergone several developments in terms of hardware and software. The first version was developed around an STM32-E407 microcontroller but this quickly proved to be insufficient for everything I wanted to implement, both in terms of hardware and firmware features.
The current version uses a **Raspberry PI 4** with at least 2GB of memory for the **ARO-Master box** and uses **RP2350** microcontrollers for the **Pier-Relay box**.

This system is in use in my personal observatories and those of some colleagues, two of which are located in Tunisia and are remotely controlled from Europe.

### Internal firmware Web Server  for magement and system setup
- No software instalation needed
- Accessible from anywhere
- OS independent using Windows, Linux, Android or Mac browser
- Auto firmware updates
- Provide an Wifi Access Point
- No need for extra Wifi router for connecting you Wifi devices (IP camera, Smart Plugs, etc) to the Internet 
- Direct integration with uAstro SkyPatroll (MSP) or uAstro Weather Station (MWS)
### Alpaca Daemon for Multiclient and MultDevice
- Alpaca Discovery aware (no setup or configuration needed)
- Implements  Dome, Switch (one for eatch pier), ObservingConditions and  SafetyMonitor
- No need to instal ASCOM drivers
- Devices can be access simultaneously from different computers
- OS agnostic, works with Windows, Linux, Android, Mac OS, etc
### Faults monitoring
- Mains voltage
- Battery voltage
- Motor current
- Weather
- External alarm
- Logged users
- Internet not available
- Temperature, humidity and dew point
- System CPU temperature 
### Other functionalities
- Watchdog reboots system on hardware/software fails
- Sends Email on Fault or roof open/close
- Coller Fan & heater control 
- Up Time. Number of minutes since the controller booted up last
### Users/Piers control
- Up to 8 piers  (one user per ‘pier’)
- Internet control of pier relays (4 relays per pier, 110/220v 10A per relay)
- No need for third-party ‘smart Wifi plugs’
- Relay reset with timed rearm
- Auto user logoff timer (turns off all relays)
- ‘Relay box’ is installed at each pier
- Daisy-chain UTP cable  pier connection, easy and less cabling
### Roof/shutter Safety – Automatic close on:
- Power fail (Mains or Battery)
- Meteo event (rain, wind, lumens, clouds)
- External signal input (first-party control)
- Optional close at Astronomical Sunrise
### Roof/shutter Safety – Prevent open on:
- If ‘Emergency’ button pressed
- Setup option ‘Enabled’ is not active
- No Meteo source present
- No Users logged in
- No Internet detected
### Roof/shutter Control
- Manual Open and Close buttons
- Manual Emergency/stop button
- Roof moviment Timeout, if no position reatched (ex: limit switch fails) in the givem time them stop motor
- Roof response Timeout, if no actual movemmente (ex: motor stall, limit switch fails, etc) in the givem time them stop motor
- Internal PWM motor control with programable Frequency, Start Duty, Max Duty, Acell ramp
- External (first-party) motor control using relay signals
### Power suply & UPS
- Switching 12v power supply with 350W
- Integrated UPS for interrupted motor operation
- Integrated battery charger (external battery)
