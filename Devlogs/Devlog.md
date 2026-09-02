# Drone Development Log

## Day 1: Research and Initial Design

Concept board: <https://app.idroo.com/boards/iBzdX5M0Z2>  
Drone General Design, Part 1: <https://lapse.hackclub.com/timelapse/2bgpf7khk9ri>

This project turned out to be much harder than I initially expected. At first, I thought designing a drone frame would mostly be about getting the dimensions right and fitting the electronics inside. Instead, almost every design choice affects several others. The frame layout determines the electronics placement, which changes the center of gravity, battery location, cooling, cable routing, and manufacturing process.

### Reference Frames

The first step was reviewing existing drones that meet my requirements: a 10-inch quadcopter capable of carrying a companion computer and depth camera while running on a 4–6S battery.

I chose the **Holybro X500 V2 / PX4 Vision Dev Kit V1.5** as my primary reference. I also reviewed the iFlight Helion 10 and AOS UL10 V5, but the Holybro platform is closer to the autonomous robotics platform I want to build.

Useful references:

- <https://docs.px4.io/main/en/frames_multicopter/holybro_x500v2_pixhawk6c>
- <https://docs.px4.io/main/assets/payloads_x500v2.BlKS32-f.png>
- <https://ntu-aris.github.io/ntu_viral_dataset/images/hardware.jpg>
- <https://docs.px4.io/main/assets/hero_image.DGHv_vvL.png>

The Holybro design also helped me understand how professional development drones package their electronics.

### Initial Design Decisions

The drone will use an X-configuration quadcopter layout. I chose this layout because it provides symmetrical flight characteristics and is common in autonomous drones. It will use a **Pixhawk 6X with the Holybro Jetson Baseboard**, allowing the flight controller and companion computer to work together as one stack.

This is an autonomous robotics platform rather than a racing drone. A depth camera such as an Intel RealSense or Luxonis OAK-D already provides RGB and depth sensing, so a separate forward-facing camera may not be necessary. The drone will also include GPS, an RC receiver, telemetry, and possibly a video transmitter.

### Mechanical Analysis

Before committing to frame dimensions, I want to perform basic engineering calculations instead of relying purely on intuition. These will include a stress analysis of the arms and a simple drop-test calculation for rough landings or crashes.

References:

- <https://sites.bu.edu/uav/files/2017/11/Frames.pdf>
- <https://blog.uavmodel.com/how-to-design-and-3d-print-custom-drone-frames/>

### Material Selection

Carbon fiber is the obvious final material because of its excellent stiffness-to-weight ratio. I will probably prototype using cheaper materials first, verify the fit, and manufacture the final version from carbon fiber later.

### Notes and Decisions

- A standard 10-inch propeller has a diameter of 254 mm, which is a useful starting point for estimating the wheelbase.
- The complete Pixhawk 6X, Jetson Baseboard, Orin NX, and heatsink assembly is approximately **126 × 80 × 39–45 mm**. This almost determines the minimum size of the center frame.
- I chose four separate ESCs instead of one 4-in-1 ESC. Separate ESCs are easier to replace, distribute heat better, and suit a research platform where reliability matters more than saving a few grams.
- The arms will be sandwiched between the upper and lower carbon plates.
- The ESCs, switching regulators, and high-current battery wiring are the main sources of electrical interference, rather than the Jetson itself.

The frame concept uses two levels. The Jetson Baseboard, telemetry, and receiver will be mounted on the upper deck. The lower section will contain the power distribution board and four ESCs. The battery will be mounted underneath, the depth camera will sit at the front, and the GPS will probably be mounted on a rear mast to reduce interference.

![Design 1](<Images/Screenshot 2026-08-05 091354.png>)

At this stage, I expect many decisions to change. The goal is to make enough informed choices to begin modeling in Fusion 360 rather than researching indefinitely.

## Day 1, Part 2: Second Design Concept

Drone General Design, Part 2: <https://lapse.hackclub.com/timelapse/HdxbJGZdjz3A>

I created a second design concept and placed the major components at approximately their real dimensions. The goal was to check whether everything could realistically fit inside the central body before starting the detailed CAD work.

The battery remains underneath the frame. The upper section is reserved for the Pixhawk 6X, Jetson Baseboard, cellular radio, RC receiver, GPS/compass, and other electronics. The four separate ESCs are placed closer to the arms to reduce motor-wire length and simplify replacement.

The Pixhawk and Jetson assembly is larger than expected, so the center frame will probably need to be larger than originally planned. Cable routing, cooling, and maintenance access are just as important as fitting the components themselves.

![Design 2](<Images/Screenshot 2026-08-05 150327.png>)

![Design 1 and Design 2 side by side](<Images/Screenshot 2026-08-05 150440.png>)

**TODO:** Plan the wiring.

## Day 2: Electronics Architecture and Schematic

Drone General Design, Part 3: <https://lapse.hackclub.com/timelapse/EFwJGuFalmob>  
KiCad Symbols: <https://lapse.hackclub.com/timelapse/CfTy0n8EebXS>  
Routing and Components: <https://lapse.hackclub.com/timelapse/v2zys5-Etka2>

I worked on the electronics and communication architecture. After comparing telemetry radios with 4G/5G communication, I decided to move toward a 4G/5G solution.

I created the initial BOM and updated several components as I found options that fit the project better. For KiCad, I made simplified symbols that expose high-level connectors instead of every individual pin. This keeps the schematic focused on system architecture rather than PCB-level detail.

![All new elements](<Images/Screenshot 2026-08-06 212505.png>)

I also studied the connectors and ports on the Pixhawk Jetson Baseboard.

Reference: <https://docs.px4.io/main/assets/power1_one_battery_3s_4s.BwKdxwes.jpg>

### Design Version 3

The third design iteration uses more realistic component dimensions and placements.

![Design Version 3](<Images/Screenshot 2026-08-07 012809.png>)

### Schematic Version 1

The first complete system schematic is intentionally high-level. It shows how the main subsystems connect without detailing individual signals or PCB-level connections.

![Schematic Version 1](<Images/Screenshot 2026-08-07 012645.png>)

Some connector and communication choices are still uncertain, so the schematic may change as the design develops. Creating it was worthwhile because it provides a map of the system before the physical wiring is finalized.

## Day 3: Real Connectors and Hardware Selection

Real Connectors: <https://lapse.hackclub.com/timelapse/CkFQIcG4ptSY>  
Finalizing Hardware Choices: <https://lapse.hackclub.com/timelapse/vVLvC90nyClp>  
Downloading and Uploading Components: <https://lapse.hackclub.com/timelapse/R_qcUxAQv0iU>  
D-Link D501 5G USB Adapter: <https://lapse.hackclub.com/timelapse/Ui7_f7U2WzdP>

I moved from theoretical hardware planning to physical placement. I placed the connectors in their approximate locations to check alignment and fit.

For propulsion, I estimated a total weight of 3.2 kg and a target thrust-to-weight ratio of 2.3:1. This requires approximately 7.4 kg of total thrust, or 1.85 kg per motor. I decided to target approximately 2 kg per motor for additional margin.

I compared 10-inch and 12-inch propeller setups using manufacturer thrust tables rather than choosing only by KV and motor size. For now, I am using 12-inch, two-blade propellers with a 6S battery and looking at motors in the 350–700 KV range.

I also downloaded 3D models for the components. Some models are approximate, but they are sufficient for checking layout. The assembly is becoming heavy for my laptop, so model optimization may be necessary.

![Power](<Images/Screenshot 2026-08-07 231127.png>)
![Communication](<Images/Screenshot 2026-08-07 231739.png>)
![ESC](<Images/Screenshot 2026-08-07 232015.png>)
![Navigation](<Images/Screenshot 2026-08-07 232129.png>)
![Propulsion](<Images/Screenshot 2026-08-07 232319.png>)
![Vision](<Images/Screenshot 2026-08-07 232448.png>)
![All components](<Images/Screenshot 2026-08-07 233741.png>)

The D-Link D501 5G USB Adapter was the only missing component, so I created an approximate model myself.

![D-Link D501 5G USB Adapter](<Images/Screenshot 2026-08-08 002027.png>)

## Day 4: Plates and Cellular Communication

Top and Bottom Plates: <https://lapse.hackclub.com/timelapse/v_VVVfQ6t21S>

Design Version 4 started to look like an actual drone, but the bottom plate still needed work. I also realized that the D-Link 5G adapter was too large and would occupy too much space. I considered moving the UBEC or placing the cellular hardware on the upper deck.

Placing every component at its real size exposed spacing and alignment problems that were not visible in the schematic. I also learned that carbon fiber can interfere with RF signals, so antenna placement and the surrounding structure will need careful consideration.

I began investigating the smaller LTE EG25-G Mini PCIe module with a USB carrier as a possible replacement for the large USB adapter.

![Design V4](<Images/Screenshot 2026-08-08 222602.png>)
![LTE EG25-G Mini PCIe adapter](<Images/Screenshot 2026-08-09 013647.png>)
![Top and bottom plates](<Images/Screenshot 2026-08-09 020030.png>)

## Day 5: Propulsion and Design Version 5

Design Version 5: <https://lapse.hackclub.com/timelapse/LQik73zLpkbC>

I worked on propulsion, including CW and CCW propellers, motor alignment, and model clearances.

The bottom plate must support the upper components and the battery underneath, so it may need to be thicker than the top plate. I also started using the PWM extension board, which required changes to the layout but provides a cleaner way to connect the four ESCs.

![Propulsion elements](<Images/Screenshot 2026-08-10 000604.png>)
![PWM extension board](Images/18118-1_1800x1800.jpg)

Remaining considerations included custom PWM connector placement, center of mass, mounting hardware, clearance checks, and battery balance.

![V5 Design Fusion](<Images/Screenshot 2026-08-10 015751.png>)
![V5 Design Layout](<Images/Screenshot 2026-08-10 021141.png>)

## Day 6: GPS, Depth Camera Mount, and Center of Mass

I created a GPS mounting base with M2 threads and a custom mount for the depth camera.

![GPS mounting base](<Images/Screenshot 2026-08-22 145932.png>)
![GPS mount with M2 threads](<Images/Screenshot 2026-08-22 150639.png>)
![Full GPS view](<Images/Screenshot 2026-08-22 150810.png>)
![Initial centers of mass](<Images/Screenshot 2026-08-22 160317.png>)
![Top plate center of mass](<Images/Screenshot 2026-08-22 160552.png>)
![Lower plate center of mass](<Images/Screenshot 2026-08-22 160644.png>)

The first center-of-mass results were approximate because the models used incorrect materials and masses. I gathered the real masses, calculated the volumes of the components, and created custom materials with matching densities in Fusion 360.

I also considered using Autodesk CFD to investigate airflow and cooling. CFD may help evaluate ventilation and external airflow, but it will not replace a careful center-of-mass calculation. The most useful next steps are to model the correct masses, check the complete assembly, verify the battery position, and test cooling around the ESCs and regulators.

I finished the depth-camera mount and added ventilation holes and mounting points.

![Finished depth camera mount](<Images/Screenshot 2026-08-22 202512.png>)
![Custom-density material setup](<Screenshot 2026-08-22 232312.png>)
![Centered lower-deck center of mass](<Images/Screenshot 2026-08-22 234318.png>)

The top-deck center of mass is nearly centered. The lower deck was initially offset, but moving the battery improved the alignment. Small ballast weights could be useful for final balancing, but they should be a last resort. It is better to correct the component layout first, especially along the longitudinal axis, where the battery offers a practical adjustment.

## Day 7: Decks and Arm Design

Decks and Arm Design: <https://lapse.hackclub.com/timelapse/D4Xei-P8a743>

I assembled the top and bottom decks and considered several support designs. I chose a tractor configuration because it is more conventional and avoids the additional drag associated with a pusher configuration.

The arms will be integrated with the lower deck while remaining modular enough to replace. I initially considered a true 90-degree X layout, but the depth camera’s field of view made that risky. A wider arm arrangement should reduce the chance of the propellers appearing in the camera’s view.

![Assembled frame](<Images/Screenshot 2026-08-25 001930.png>)
![First arm attempt](<Images/Screenshot 2026-08-25 021229.png>)
![Second arm design](<Images/Screenshot 2026-08-25 022238.png>)

## Day 8: Arms and Motors

Arms and Motors: <https://lapse.hackclub.com/timelapse/MWGjAlClZqYt>

I worked on the arms and motor placement, ensuring that the propellers remain outside the depth camera’s field of view. A computational error in the original sketch made mirroring and positioning difficult, so I created a projection sketch and corrected the geometry.

I also realized that I had accidentally started designing a true X instead of the Deadcat configuration I originally wanted. The corrected approach is to draw the propeller positions and viewing clearances first, then design the arms around them.

## Day 9: Arm Geometry and Center of Mass

Arm Geometry and Center of Mass: <https://lapse.hackclub.com/timelapse/7mI4HmFSVszn>

The first arm layout failed because it did not account for the camera, opposing propellers, and neighboring propellers. I also tried to make all the arms meet at one point, which created unnecessary center-of-mass constraints.

The revised design is a **stretched-rectangle Deadcat** configuration. I started with the propeller positions and angles, then designed the arms around those constraints. This made it easier to keep the camera view clear and avoid propeller overlap.

![Neighboring propellers overlapping](<Images/Screenshot 2026-08-28 190242.png>)
![Arm layout](<Images/Screenshot 2026-08-28 200513.png>)
![Center-of-mass calculation](<Images/Screenshot 2026-08-28 210831.png>)
![Preliminary arm](<Images/Screenshot 2026-08-28 214018.png>)

I added motor protection and refined the arm geometry. The motor area needed more width, and the edges needed to be smoother. I also kept a safety margin around the screw holes: the material between a hole and the outer edge should be at least as wide as the hole diameter.

![Arm-tip reference](<Images/Screenshot 2026-08-28 214935.png>)
![Full arm](<Images/Screenshot 2026-08-28 223953.png>)
![Refined arm geometry](<Images/Screenshot 2026-08-28 232143.png>)
![Front arms](<Images/Screenshot 2026-08-28 233744.png>)
![Complete arm sketch](<Images/Screenshot 2026-08-28 233822.png>)
![Arm detail](<Images/Screenshot 2026-08-28 233833.png>)

## Day 10: Rear Arm Geometry and Mirroring

Rear Arm Geometry and Mirroring: <https://lapse.hackclub.com/timelapse/CoAkKe85k_lb>

I modified the frame base to reduce weight and created the rear arm. The rear arms are at different angles relative to the base, so directly mirroring the front arm would not produce the correct motor position. I recreated the basic rear-arm geometry using the correct dimensions and angle, then copied and rotated the more complex features.

![Mirrored rear arm](<Images/Screenshot 2026-08-28 233822.png>)

The first rear-arm attempt failed because the alignment and width did not match. The remaining task was to clean the old dimensions and make the arms symmetrical.

## Day 11: Arm Frames and Modular Mounting

Arm Frames and Modular Mounting: <https://lapse.hackclub.com/timelapse/jwxJgQtA3ZOm>  
Arm Frame Plane and Weight Reduction: <https://lapse.hackclub.com/timelapse/I-VWwIf2Bi_W>  
Arm Aerodynamics and Integration: <https://lapse.hackclub.com/timelapse/D9md9M-yNeOV>

After fixing duplicated geometry and several alignment problems, I connected the arm bases. The goal is to make the arms stiff while keeping them swappable. The front and rear arm frames connect to the body, but remain independent enough to remove without disassembling the entire drone.

![Right arm plane](<Images/Screenshot 2026-08-31 151422.png>)
![Mirrored drone](<Images/Screenshot 2026-08-31 152903.png>)

The arm planes use interlocking notches for alignment while remaining separate parts. I corrected the mirrored geometry, searched for gaps in the sketch, and finished the main arm-plane design.

![Finished arm plane](<Images/Screenshot 2026-09-01 040221.png>)
![Arm plane, alternate view](<Images/Screenshot 2026-09-01 041004.png>)
![Arm plane, bottom view](<Images/Screenshot 2026-09-01 041058.png>)

The remaining work was to add mounting screws and supports for the upper deck.

## Day 12: ESC Integration and Final Frame

ESC Integration and Final Frame: <https://lapse.hackclub.com/timelapse/t7EPD3rolfCb>  
CFD Flow Simulation Test: <https://lapse.hackclub.com/timelapse/_f0_-MtugOYQ>

I added mounting holes and finished connecting the bottom and arm planes.

![Mounting holes](<Images/Screenshot 2026-09-02 000307.png>)
![Arm-plane mounting](<Images/Screenshot 2026-09-02 001133.png>)
![Bottom and arm planes](<Images/Screenshot 2026-09-02 004459.png>)

I had initially forgotten the ESCs, so I redesigned part of the arm to integrate them properly. The ESCs are now mounted, and I started creating the supports for the upper deck and a cover for the RC receiver.

![ESCs mounted](<Images/Screenshot 2026-09-02 020452.png>)
![Side view](<Images/Screenshot 2026-09-02 044739.png>)
![Top view](<Images/Screenshot 2026-09-02 044817.png>)
![Side view 2](<Images/Screenshot 2026-09-02 044905.png>)
![Lower plane](<Images/Screenshot 2026-09-02 044954.png>)
![Arm plane](<Images/Screenshot 2026-09-02 045237.png>)
![Side view 3](<Images/Screenshot 2026-09-02 051722.png>)
![Front view with LiPo](<Images/Screenshot 2026-09-02 051736.png>)

I added ventilation holes for aerodynamics and cooling, applied the final fillets, and placed the LiPo battery. The main frame is now complete, and the next step is to finish exporting the model and continue with CFD testing.
