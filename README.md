# Custom Drone
hey! this is my custom quadcopter/uav that ive been designing from scratch over the last few months.

the goal is to make a relatively compact quadcopter that can carry a bunch of sensors and a jetson computer while still having enough thrust and flight time to actually be useful.

the whole frame is designed in Fusion 360 and im planning to manufacture the main structural parts from carbon fiber.

![Full drone](<Devlogs/Images/Screenshot 2026-09-02 051722.png>)

## Reviewer note

Hey! If you're reviewing this, the main thing I would look at is the CAD design and how the different parts were integrated together. I tried to design the frame around the actual components instead of just making something that looks cool.

There are probably still some things I could improve, especially around weight, rigidity and aerodynamics, but I wanted to get a complete working design first and then improve it from there. Thanks for checking it out! :)


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

![Schematics](<Screenshot 2026-08-07 012645.png>)

also i just wanted to see how far i could take a drone design in CAD before actually building it.

## how i made it

most of the mechanical design was done in **Autodesk Fusion 360**.

i started with the overall frame dimensions and then worked from the propellers inward. this ended up being way better than trying to randomly draw the arms first because propeller clearance becomes a huge pain very quickly.

the frame went through quite a few versions.

at one point i accidentally designed a normal X layout when i was actually trying to make a deadcat layout, which was fun to figure out later.


![X](<Devlogs/Images/Screenshot 2026-08-25 022238.png>)

after that i worked on the arm angles, motor positions, camera clearance and center of mass.

the center of mass was another thing that took way more work than i expected. i used the actual component masses where i could and adjusted the material densities in Fusion so the CAD model would represent the real components better.

![lower plane](<Screenshot 2026-08-22 232843.png>)

i also made the arm sections modular so they can be removed/swapped without having to completely take apart the whole drone.

## frame design

the frame has separate top, bottom and arm planes.

the bottom section carries a lot of the main structure and battery, while the top section is mainly for electronics and mounting.

i added mounting points for the different components and also added holes in the top plate to remove some material and hopefully improve airflow.

the arms also got redesigned after i realized i had completely forgotten about the ESCs.

![epic fail](<Devlogs/Images/Screenshot 2026-09-02 001133.png>)

yes.

i designed the arms and then remembered that the ESCs probably needed somewhere to go.

so i had to redo part of the arm design and integrate the ESC mounting properly.


![top view](<Devlogs/Images/Screenshot 2026-09-02 045237.png>)


## center of mass

the current estimated drone mass is around **3.2 kg** including some extra allowance for wiring, heatshrink and other small stuff.

i was aiming for roughly a **2.3:1 thrust-to-weight safety ratio**, which gives a target total thrust of around 7.4 kg.

that means around 1.9–2.0 kg of thrust per motor.

the battery position is also being used as one of the main ways to adjust the final center of mass instead of just adding random ballast weights.

## CFD

i am also testing the final drone design using CFD. But more experimentation are for the future.

## some pictures

![top](<Devlogs/Images/Screenshot 2026-09-02 044954.png>)

![side view](<Devlogs/Images/Screenshot 2026-09-02 044905.png>)

![front view](<Devlogs/Images/Screenshot 2026-09-02 051736.png>)

![top 2](<Devlogs/Images/Screenshot 2026-09-02 044817.png>)

![arms plane](<Devlogs/Images/Screenshot 2026-09-02 045237.png>)

![lower plane](<Devlogs/Images/Screenshot 2026-09-02 044954.png>)