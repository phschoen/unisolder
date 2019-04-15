# unisolder

![unisolder52](https://raw.githubusercontent.com/phschoen/unisolder/master/pics/unisolder52.jpg "unisolder52")

The intention was to build the most universal soldering controller I can think of.
It can drive any low voltage (upto 24V) iron with thermocouple or resistive sensor,
in series with the heater, or separate.

Here is a short list of features:
- power: 9-28V, AC or DC
- 2 separate heater control channels
- 2 independent sensor inputs
- current source on any sensor input 3uA - 12mA, wuth 2 bands (x1, x16) and 256 steps per band
- flexible differential amplifier input selection
- amplifier gain from 0 to 750 in 256 steps
- negative offset selection in 1024 steps
- resistive instrument identification (upto 625 different instruments can be identified by 2 resistors on the connector)
- polynomial floating point voltage/resistance to temperature calculation
- wave shaping to filter out the inductive peaks from series sensor signal
- PID control with power limit
- isolated USB port for firmware updates and live data
- 128x64 OLED display with rich user interface.

Tested so far with:
- HAKKO T12/T15 (series TC)
- HAKKO FX8801 (PTC)
- PACE TD100 (series TC)
- JBC C245 (series or separate TC)
- JBC C210 (series TC)
- JBC Microtweezers (2 separate heaters, each with series TC)
- WELLER WSP80 (PTC) (This iron was sent to me by a reader of the thread for a previous version of the controller. Thanks, Jaroslaw)
- ERSA RT80 (series PTC/heater resistance)
- various chinese cheap irons with separate TC

## Update (4 April 2017): 
The PC Software is now entirely in C#, the front end is rewritten. Now you can program only the bootloader,
and then use the software for firmware updates using the USB connection. The PC software also does not crash
anymore when device is unplugged and plugged in the USB or turned on/off, and automatically switches to
bootloader and back when uploading new firmware. Also, a legend with checkboxes is added for every data
that is displayed on the graph, so you can switch it on or off. There is still pretty much work to be done on it,
but at least it is much more functional now.
Added to the firmware are Pace TD100 Black and Weller WMRT profiles, some work is done on several other places.
Now the firmware handles better some irons, where there was initial overshoot when heating for the first time
or changing the target temperature.

Some movies:
 - [JBC C245](https://www.youtube.com/watch?v=oTdQB4ywDOA)
 - [JBC C210](https://www.youtube.com/watch?v=iyz-EDf-JaY)
 - [T12, JBC C210, JBC Microtweezers](https://www.youtube.com/watch?v=-f0KSU0PJzc&t=70s)
 - [Chinese T12](https://www.youtube.com/watch?v=u588sh-4thg)
 - [Weller WSP80](https://www.youtube.com/watch?v=gd_8w7l8_Bo)
 - [Weller WMRT](https://www.youtube.com/watch?v=eHNJuQEw6XU)

The content of this is originaly copied thanks to sparkybg from [dangerousprototypes.com](http://dangerousprototypes.com/forum/viewtopic.php?t=7218)

## Connections to different tips/irons:

1. HAKKO T12:
- Outer shell, and heater negative (middle) terminal connected together to Vout1- and EARTH
- heater positive (bottom terminal) connected to Vout1+ and SENSEA
- 1k resistor between ID and Vout1-
- 5.6k resistor between ID and Vout2-

2. HAKKO FX8801, HAKKO 907 (original, with PTC sensor):
- Outer shell, PTC negative and heater negative connected to EARTH, Vout1- and SENSEB
- Heater positive connected to Vout1+
- PTC positive connected to SENSEA
- 1k between ID and Vout1-
- 820ohm between ID and Vout2-

3. JBC C245:
- Outer shell (green wire) connected to EARTH and SENSEB
- Heater positive(red wire) connected to Vout1- and SENSEA
- Heater negative(blue wire) connected to Vout1+
- 150ohm between ID and Vout1-
- 5.6k between ID and Vout2-

4. JBC C210:
- Outer shell (green wire) connected to EARTH and SENSEB
- Heater negative (middle terminal, blue wire) connected to Vout1-
- Heater positive (smaller terminal, red wire) connected to Vout1+ and SENSEA
- 3.0k between ID and Vout1-
- 5.6k between ID and Vout2-

5. JBC Microtweezers:
- Outer shell of both tips (green wire) connected to EARTH
- Heater 1 negative (blue wire) connected to Vout1-
- Heater 1 positive (red wire) connected to Vout1+ and SENSEA
- Heater 2 negative (brown wire) connected to Vout2-
- Heater 2 positive (yellow wire) connected to Vout2+ and SENSEB
- 1.0k between ID and Vout1-

6. WELLER WSP80:
- Outer shell, PTC negative and heater negative (white, black and brown wires) connected to EARTH, Vout1- and SENSEB
- Heater positive (blue wire) connected to Vout1+
- PTC positive (red wire) connected to SENSEA
- 120ohm between ID and Vout1-
- 5.6k between ID and Vout2-

7. ERSA RT80:
- Outer shell and Heater/PTC negative (pink and white wires) connected to EARTH, Vout1- and SENSEB
- Heater/PTC positive (black wire) connected to Vout1+ and SENSEA
- 300ohm between ID and Vout1-
- 110ohm between ID and Vout2-

see also https://github.com/5N44P/unisolder-notes
