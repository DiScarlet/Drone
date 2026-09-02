# Custom Drone
hey! this is my custom quadcopter/uav that ive been designing from scratch over the last few months.

the goal is to make a relatively compact quadcopter that can carry a bunch of sensors and a jetson computer while still having enough thrust and flight time to actually be useful.

the whole frame is designed in Fusion 360 and im planning to manufacture the main structural parts from carbon fiber.

![Full drone](<Devlogs/Images/Screenshot 2026-09-02 051722.png>)

## what is this?

this is a custom 11 inch drone with a stretched/deadcat style frame.

the drone is designed around:

- Pixhawk Jetson Baseboard
- Jetson Orin NX/Nano
- Holybro M10 GPS + IST8310 compass
- 4 individual ESCs
- 4 motors
- 11–12" propellers
- 6S battery
- depth camera
- 4 LiDAR sensors
- 4G communication

the idea is to have enough room for all of this without making the frame unnecessarily huge or heavy.

## why did i make this?

i wanted to build a drone where i actually designed the frame myself instead of just buying a random frame and putting electronics on it.

there were also a bunch of things i wanted to experiment with, mainly:

- custom carbon fiber frame design
- center of mass optimization
- propeller clearance
- modular arm mounting
- sensor placement
- aerodynamic testing
- fitting a jetson computer onto a relatively small drone

also i just wanted to see how far i could take a drone design in CAD before actually building it.

## how i made it

most of the mechanical design was done in **Autodesk Fusion 360**.

i started with the overall frame dimensions and then worked from the propellers inward. this ended up being way better than trying to randomly draw the arms first because propeller clearance becomes a huge pain very quickly.

the frame went through quite a few versions.

at one point i accidentally designed a normal X layout when i was actually trying to make a deadcat layout, which was fun to figure out later.


![X](<Devlogs/Images/Screenshot 2026-08-25 022238.png>)

after that i worked on the arm angles, motor positions, camera clearance and center of mass.

the center of mass was another thing that took way more work than i expected. i used the actual component masses where i could and adjusted the material densities in Fusion so the CAD model would represent the real components better.

![lower plane](<Images/Screenshot 2026-09-02 044954.png>)

i also made the arm sections modular so they can be removed/swapped without having to completely take apart the whole drone.

## frame design

the frame has separate top, bottom and arm planes.

the bottom section carries a lot of the main structure and battery, while the top section is mainly for electronics and mounting.

i added mounting points for the different components and also added holes in the top plate to remove some material and hopefully improve airflow.

![top view](<Images/Screenshot 2026-09-02 044817.png>)

the arms also got redesigned after i realized i had completely forgotten about the ESCs.

yes.

i designed the arms and then remembered that the ESCs probably needed somewhere to go.

so i had to redo part of the arm design and integrate the ESC mounting properly.

![ESCs](<Images/Screenshot 2026-09-02 020452.png>)

## center of mass

the current estimated drone mass is around **3.2 kg** including some extra allowance for wiring, heatshrink and other small stuff.

i was aiming for roughly a **2.3:1 thrust-to-weight safety ratio**, which gives a target total thrust of around 7.4 kg.

that means around 1.9–2.0 kg of thrust per motor.

the battery position is also being used as one of the main ways to adjust the final center of mass instead of just adding random ballast weights.

## CFD

i am also testing the final drone design using CFD.

the main simulation is being done in **SimScale** using:

- Flow → Incompressible
- steady-state
- k-ω SST turbulence model
- air
- 10 m/s incoming airflow
- MRF rotating zones for the propellers

the main things im looking at are:

- airflow around the frame
- pressure distribution
- propeller wake
- velocity around the arms and camera
- drag
- thrust
- forces and moments

the point of the CFD isn't to make a pretty rainbow screenshot and call it a day. i want to see if there are any obvious problems with the frame geometry and how much the frame is messing with the airflow.

![side view](<Images/Screenshot 2026-09-02 044739.png>)

## CAD files

the CAD files are included in this repository.

to open the project, download the Fusion 360 files and open them using **Autodesk Fusion 360**.

you will need Fusion 360 to edit the CAD model.

the CFD setup is separate and is being done through SimScale.

## how to view / continue the project

### Fusion 360

1. Download the CAD files from this repository.
2. Open them in Autodesk Fusion 360.
3. From there you can inspect the individual components and modify the frame.

### CFD

the CFD simulation is set up in SimScale.

the model can be imported into a SimScale project and the simulation setup can be inspected there.

## current status

- [x] basic frame design
- [x] propeller clearance
- [x] arm geometry
- [x] camera mount
- [x] GPS mount
- [x] center of mass testing
- [x] ESC integration
- [x] top and bottom decks
- [x] modular arm mounting
- [x] RC mounting
- [x] aerodynamic holes
- [x] fillets
- [x] full frame design
- [ ] CFD analysis
- [ ] final structural testing
- [ ] final electronics layout
- [ ] carbon fiber manufacturing
- [ ] assembly
- [ ] flight testing

## some pictures

![front view](<Images/Screenshot 2026-09-02 044634.png>)

![side view](<Images/Screenshot 2026-09-02 044739.png>)

![top](<Images/Screenshot 2026-09-02 044817.png>)

![side 2](<Images/Screenshot 2026-09-02 044905.png>)

![lower plane](<Images/Screenshot 2026-09-02 044954.png>)

![arms plane](<Images/Screenshot 2026-09-02 045237.png>)

## problems i ran into

there were honestly a lot.

the arm geometry was probably the biggest one. i had problems with mirroring, constraints and the angles because my original sketch started getting computational errors.

i ended up using projection sketches to get around some of the issues.

then i had to redesign the rear arms because they couldn't just be mirrored like i originally thought.

after that i had the center of mass to deal with.

then i remembered the ESCs.

then i had to redesign the arms again.

so yeah, there were quite a few "oh shit i forgot about that" moments.

but thats also kinda the point of the project. im actually learning how to design the thing instead of just following a tutorial where everything magically works first try.

## software / tools

- **Autodesk Fusion 360** — CAD and mechanical design
- **SimScale** — CFD
- **Git / GitHub** — project files and version control

## AI disclosure

i did use AI during this project, mainly as a second opinion when i got stuck.

i used it for things like:

- checking calculations
- understanding some CAD/CFD concepts
- getting suggestions when i was stuck on a design problem
- checking technical information about some components
- helping me understand how to set up the CFD simulation

the actual CAD design, dimensions, component placement, frame layout and design decisions were made by me.

AI was not used to generate the CAD model for me.

## final note

this project is still a work in progress.

the CAD is getting close to the point where i can actually manufacture the frame, but there is still a lot to test before this thing gets anywhere near actual flight.

hopefully it works.

if it doesn't, well...

back to Fusion 360 :)