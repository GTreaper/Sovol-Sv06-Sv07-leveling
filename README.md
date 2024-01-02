# Sovol-Sv06-Sv07-leveling.
A guide on how i have achieved great first layers on the Sv06+ and Sv07+. 


# Never try to:
Home the printer without the pei plate, the sensor will not react against the magnet below it needs the steel plate on to function!

All adjustments and calibrations except BED MESH should be done with the printer cold in room temp to eliminate any thermal expansion.

DONT TOUCH THE Z-TILT BETWEEN THESE STEPS. Z TILT ONLY WHEN YOU ARE CERTAIN EVERYTHING IS LEVELED TO THE FRAME AND ALL STEPS ARE DONE.

# Adjustments/checks that should be done before:

V-Wheel adjustment:

Make sure wheels aren't too tight or lose, being able to turn them by hand but the carriage sitting firm with no play.
Clean the V-wheels and rails/extrusions properly.

Z-Axis lead screws:

Make sure to clean and lube the lead screws properly.
Check that the anti backlash nuts aren't to tighten so they can function properly.
Make sure heatblock is straight and tightened firmly as well as a nozzle.



# STEP 1: Measuring!

Start by homing the printer.
When "homing all" is done, without disabling motors!! Measure the distance from the base of the printer to the top part of X carriage. (See picture 1)
Start from the left side and note the measurement. (Make sure you are holding the caliper as straight as possible and measure twice).

Now measure the opposite side the same way on the equal spot, if its lower or higher than left side continues with the next step.
(You want the measurements as equal as possible, 0.01-0.05mm difference is acceptable but the closer the better).

picture 1:
![Step1](https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/b04fbe07-4e4d-4aa3-86c9-c451fa93d6dc)



# Step 2: Adjusting the X carrige!

Turn the lead screw by turning the coupler on the motor. There will be a slight resistance and it will feel like small steps when turning.

This is because the motor is on and not disabled, making it easier to adjust.

Turn it so the right side goes up or down depending on your measurements. When both sides are at the same height, home the printer and measure again.
(You might have to make a small adjustment again after homing that's ok).
The distance between the X carriage and frame/base of the printer should now be equal or as close as possible on both sides.


# Step 3: Ajusting the bed to the X carrige! (This step is Sv07/Sv07+ specific, for Sv06/Sv06+ see bottom of the page)

Go into the bed level menu (screw tilt) and press reference corner. DO NOT PRESS SCREW ADJUST. (see picture 2).
With the nozzle above the reference screw, do the "paper test" and adjust that screw until you are happy with the distance between the bed and nozzle. DO NOT PRESS SCREW ADJUST!

Picture 2: Refrence corner marked with yellow.

![screw tilt07](https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/309ded4c-6ad6-47cc-875b-e831f87187f6)

Home the printer (home all).
Move the bed (Y axis) so the reference screw is below the X Carriage and without any pressure on the bed measure from the bed up to the x carriage same way as previous step (note the distance).

Same principles as before applies here, measure the other side (Front right) and adjust bed using the bed screw until equal distance to the X carrige (same rules apply as before).
Do this with all corners/screws and adjust all to the same distance as the reference corner. (see picture 3).

When you are happy with the distance on all corners, do a screw adjust and in small adjustments make all screws 0.
If you wanna be fully certain repeat the meassurement steps one more time to make final adjustments.


Picture 3:
![Step3](https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/1fe192b9-c28c-4da6-9341-a29b5b64bc66)


# Step 4: Probe calibration!
Home the printer.
Now from fluid or mainsail do a PROBE_CALIBRATE by writing PROBE_CALIBRATE to the console and send. (https://www.klipper3d.org/Probe_Calibrate.html).

This will perform an automatic probe, then lift the head, move the nozzle over the location of the probe point, and start the manual probe tool.
Inside fluidd or mainsail, you should now see a window that lets you adjust the nozzle up or down, the same "paper test" applies here..

Personally I use a feeler gauge with thickness 0.100mm for this, but regular paper will work as well. When happy with the distance and a small pressure on the paper/gauge press accept, Klipper will reboot.
Do a PROBE_ACCURACY after PROBE_CALIBRATION is done. (https://www.klipper3d.org/Probe_Calibrate.html#repeatability-check).

# Before continuing!
Check your bed mesh settings, these are located in the printer.cfg. After trying and adjusting a lot, these are the current values I'm using:
(I have excluded mesh min and max as these shouldn't be changed if you haven't changed anything or are an experienced user that knows why you need to change them).

Sv06+![mesh06](https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/4c1f3f25-4c8e-46c7-a9ef-3bb9630649f5)
Sv07+![mesh07](https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/e1931046-0621-4026-aa9e-5d2bb05fd197)



7x7 as probe count usually is more than enough, I'm currently using 9x9 as a testing period.

If your bed is severely warped, then bicubic_tension might need to be lower.

Remember: when changing bed mesh settings in config new bed mesh calibration needs to be done! Save your current parameters so you can revert the settings if it doesn't work like you want it to.
Careful when editing the SV07/SV07+ to not delete any grayed out parameter. These are outcommented by sovol and shouldn't be edited.

# Step 5: PID Tuning and heating! (if you pid tuned not long ago skip the pid tuning)
I recommend to do a PID tuning on the bed and extruder (https://www.obico.io/blog/klipper-pid-tuning/).
When PID TUNING is done, turn on the heat bed to the same temperature (the temperature should be equal to your usual printing temp).
Printing PLA I always have a bed at 60c so I will use this as an example.
Heat the bed to 60c and let it heatsoak for some time (10-15min).
When bed has been heat soaked, do a bed mesh and save.

Now your printer should be leveled and have better accuracy when printing.
These measurements can be taken from time to time to make sure it hasn't started to change.

# Step 6: First layer adjustment!
When all previous steps are done, slice a first layer model sized 150x150-220x220 and print. While printing do fine adjustment to Z offset.
I usually adjust with the lowest value available on the screen or in fluidd/mainsail.. Usually 0.005+-! if I don't immediately see that it needs big adjustments.

Sometimes i find a point where i would like to have it just a tiny more up or down but 0.005 +- is to much.
If thats the case you can write in console while printing, change the x in 0.00x to the adjustment distance you want!

(example SET_GCODE_OFFSET Z_ADJUST=+0.0025 MOVE=1, notice the plus in +0.0025! This will offset Z height with 0.0025mm up from the bed).

To offset Z height up 0.0025mm:

SET_GCODE_OFFSET Z_ADJUST=+0.0025 MOVE=1

To offset Z height down 0.0025mm: 

SET_GCODE_OFFSET Z_ADJUST=-0.0025 MOVE=1

Move=1 means it should be adjusted instantly and not wait for next layerchange, this is important to see any diffrence during the first layer calibration.

# Last words!
Now you should be done.
Hope this made any sense and was easy to understand, your first layer should now be more precise and even.

Some slicer settings that can affect the first layer like gaps or ridging.
Extrusion width, I usually set this to around 110-120% of nozzle diameter.
Flow rate, under extrusion can create gaps due to line width not being correct.
Flkow rate, Over extrusion can make lines overlap too much and create ridges.
Infill/wall overlap %, usually have it set between 30-45%.

If you have any question, I will try to answer them as good as possible.



# Step 3 info on Sv06/Sv06+.
Since this printer has a "non adjustable" bed this cant be done the same way! But there is a common and simple mod to get a super flat bed and bed mesh on these.
Silicone mod as its called, find more info about it here: https://sv06.blakadder.com/Upgrades/silicone-mod/
Doing this before anything else will greatly improve the performance of the Sv06/Sv06+.





# Video on my printers putting down first layers!
https://github.com/GTreaper/Sovol-Sv06-Sv07-leveling./assets/99057390/058156c6-f4a0-4eac-a5d2-d20189e29a8e

