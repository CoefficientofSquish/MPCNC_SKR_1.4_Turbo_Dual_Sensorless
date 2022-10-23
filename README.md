# MPCNC_SKR_1.4_Turbo_Dual_Sensorless
Marlin firmware for MPCNC Primo with BTT SKR 1.4 Turbo, TMC 2209 stepper drivers, and dual sensorless homing

 ![SKR1 4_T_Markup](https://user-images.githubusercontent.com/77234250/197414940-23d065cf-c6c3-494d-aec5-0d1fe1516a99.png)

-----------------------------------------------------------------------
Some info about the .bin file:

-Sensorless Homing enabled for X and Y axis, Z min set up for fix mounted probe or touchplate ("Fix_Mounted_Probe" enabled in config file and set to Z-Min pin).    
    G28 command will home X and Y, then Z in the center of the build surface so make sure to be ready with touchplate unless you have a fix mounted probe.

-X and Y endstops are active for both motors on each axis, dual endstops.  The stallguard sensitivity is set to 80 which is pretty high, but has triggered pretty accurately for me.

-M3/M5 Spindle enabled with RPM speed (0-30,000) rather than PWM (0-255). PWM_ENA_PIN and PWM_PIN are set to the same pin (2_05) with no PWM_DIR_PIN, since I don't need to be able to change my spindle direction.  Wire spindle +/- to hotbed +/- pins according to BTT diagram and use M3 S(0-30000)/M5 to control spindle speed.  So far it is cutting with no issue, as long as you ramp it up at the start of a job by giving command M3 (no arguments) and then bring it up to full speed after some delay from within your G-Code (M3 S30000). 

-Asynchronous Laser mode enabled for 2-wire PWM lasers, connect to Heater 1 according to BTT diagram and control laser with M106 S(0-255)/M107.  Pins for Fan0 and Heater1 are swapped because I burned up my fan MOSFET, probably with the laser, and its probably just a better idea to use that MOSFET for the laser anyway, even if you haven't burned yours up yet.

-G29 Auto Bed Leveling enabled (Bilinear).  Make sure touchplate or Z Probe is connected and G29 P1 will create a mesh of your build surface with 16 points, just like on a 3D Printer.  You will need to follow the spindle or tool around with the touchplate to each of the 16 probing points or use a plate large enough to cover the whole build surface.  I used the side piece of a desktop PC enclosure as one big touchplate but I still had to move it around for a few of the points because my build surface is 480mmx360mm.

-----------------------------------------------------------------------------------------------------------------------

I'm including the configuration.h, configuration_adv.h and pins_BTT_SKR_common.h files in case anybody needs to modify for their own purposes and I'll do my best to update them as new versions of Marlin are released.  If you do need to compile your own make sure you use all three files or the pin assignments won't be right for the laser.  It should still work but you'll connect your laser to the default Fan0 pin instead of the extruder pin (and probably burn up your fan mosfet, at which point you'll definitely have to recompile using my pins file or reassign them yourself).   

If you use these configurations please let me know how they worked for you, or if you have any problems with it.  So far everything seems to be working properly with my build.
