# MPCNC_SKR_1.4_Turbo_Dual_Sensorless
Marlin firmware for MPCNC Primo with BTT SKR 1.4 Turbo, TMC 2209 stepper drivers, and dual sensorless homing
 

Some info about the .bin file:

-Sensorless Homing enabled for X and Y axis, Z min set up for touchplate.    G28 command will home X and Y, then Z in the center of the build surface so make sure to be ready with touchplate unless you have a fix mounted probe.

-X and Y endstops are active for both motors on each axis, dual endstops.  The stallguard sensitivity is set to 80 which is pretty high, but has triggered pretty accurately for me.

-M3/M5 Spindle enabled with RPM speed (0-30,000) rather than PWM (0-255).  Wire spindle to hotbed pins according to BTT diagram and use M3 S(0-30000)/M5 to control spindle speed.  

-Asynchronous Laser enabled for 2 wire PWM lasers, connect to "CNC Fan" according to BTT diagram and control laser with M106 S(0-255)/M107.

-G29 Bed Leveling enabled.  Make sure touchplate or Z Probe is connected and G29 P1 will create a mesh of your build surface, just like on a 3D Printer.  You will need to follow the spindle or tool around with the touchplate to each of the 16 probing points or use a plate large enough to cover the whole build surface.  I used the side of a desktop PC enclosure as one big touchplate but I still had to move it around for a few of the points.



I'm including the configuration.h and configuration_adv.h files in case anybody needs to modify for their own purposes.  If you use these configurations please let me know how they worked for you, or if you have any problems with it.  So far everything seems to be working properly with my build.
