# DU-Space-Elevator
Space elevators for DU

### Shaft Edition

This is a typical elevator meant for use in a shaft and can work with hovers or vboosters installed at an angle, pointing at walls on all sides.  Example shown here - note that you likely need 2 hovers/vboosters per corner to keep everything centered
![Elevator Setup Example](/SpaceExampleSetup.png)

![Elevator Screen Example](/ElevatorScreenExample.png)

You will also likely need lateral thrusters - thrusters pointing north, east, south, west, which help keep it centered within the shaft in situations where the hovers can't do so without causing undesired altitude changes.  

Like most space elevators, the advantages here are that hovers and vboosters are fuel efficient, and can give great power and speed for their size and cost, as long as you have a shaft all the way up.  It is capable of taking multiple altitudes as stops and cycling between them, and hovering at the given altitude.

The same script works in an ECU and offers all the same functionality, but you can enter build mode while controlling only an ECU

## Setup

It's a little rough right now.  

1. Place the elevator exactly where you want it - we need to get its position and facing that it will try to align to, so make sure it's centered and straight.  
2. Connect up either 2 buttons for up/down that goes immediately, 3 buttons for up/down to select a destination and the third button to go there, or a screen
3. Download and run the autoconfigure on a Remote Controller
4. Start the remote, then turn it off.  Some text should print to your lua console.  Screenshot or copy this text
5. In Unit.Start (I suggest editing the autoconf for yourself to make it easier to work with), find `--StartPosition = vec3({14770.396517333,98528.785329159,-48951.873671012})`
6. Replace these numbers with the ones given in your print and remove the dashes.  Add two dashes in front of the next line that says `StartPosition = vec3(core.getConstructWorldPos())` (and in front of the print if you want)
7. Find `--Forward = vec3({0.76004380107695,0.32697215931749,-0.56162515607693})`
8. Replace these numbers with the ones given in your print and remove the dashes.  Add two dashes in front of the next line that says `Forward = vec3(core.getConstructWorldOrientationForward())` (and in front of the print if you want)

And finally, setting up the floors is relatively simple past that.

1. In Unit.Start, find `Positions = {254,273,290,305,322,338,355,371}`.  These are examples - each one is the altitude of a stop on the elevator.  You may delete the numbers inside the brackets to show `Positions = {}`
2. Put in the altitude (shown on your HUD) when standing at each intended position, starting with the elevator's starting altitude - for example if the elevator's ground floor is at 20m altitude and you want to go to 1000m, you would have `Positions = {20,1000}`
3. In Unit.Start, find ` PositionNames = {"Public Area", "Ingots & Alloys", "Parts Manufacture", "Mechanism Manufacture","Floor 4 WIP","Floor 5 WIP", "Floor 6 WIP", "Floor 7 WIP"}`.  These are examples - each one is the name of a stop you just defined in the previous step.  You may delete the everything inside the brackets to show `PositionNames = {}`
4. Fill in the names of your positions, in order, with quotes around them as in the example.  You must have the same number of position names as you have positions.

That's it, your elevator should be ready to go script-wise

## Elevator Setup

Your elevator will need, as described before, hovers facing the walls at an angle.  It is best if these are symmetrical and the walls are at least 1-2 voxels from the edge of the elevator.  You will need adjustors for all directions to keep it level and facing the right way.  You will need air (and space) brakes.  You will probably need lateral engines, atmo and space, facing in each direction to help keep it centered.


# Warnings and Caveats

## This elevator is not actually tested in space yet.  We're getting there

Otherwise, you may set the MaxSpeed lua parameter to control the max vertical speed in m/s.  Going too fast may cause it to hit the sides of the shaft and have problems.  There may be problems depending on your particular setup.

It overshoots its destination by a few meters when going up currently on my test elevator, even though I've already destroyed the math to make it not.  I don't know what it will do on heavier elevators, which it didn't used to do.  But I think this is a good tradeoff for the smoother hovering and centering
