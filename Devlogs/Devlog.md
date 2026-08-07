
# Devlog #1 – Research & Initial Design

Link to the board where i drew the concept : https://app.idroo.com/boards/iBzdX5M0Z2
Drone General Design : Part 1 https://lapse.hackclub.com/timelapse/2bgpf7khk9ri

This project turned out to be much harder than I initially expected. At first, I thought designing a drone frame would mostly be about getting the dimensions right and fitting the electronics inside. Instead, almost every design choice affects several others. The frame layout determines the electronics placement, which changes the center of gravity, which then affects the battery location, cooling, cable routing and even manufacturing. I already know that I'll probably redesign a lot of things later, but for now I just need to make enough decisions to start modeling.

## Reference Frames

The first step was looking at existing drones that meet my requirements: a **10-inch(i'll test it later) quadcopter capable of carrying a companion computer and a depth camera while running on a 4–6S battery**.

After looking through different options, I decided to use the **Holybro X500 V2 / PX4 Vision Dev Kit V1.5** as my primary reference. I also looked at the iFlight Helion 10 and AOS UL10 V5, but the Holybro platform is much closer to what I want to build because it is designed for autonomous robotics rather than FPV racing.

Useful references:

* [https://docs.px4.io/main/en/frames_multicopter/holybro_x500v2_pixhawk6c](https://docs.px4.io/main/en/frames_multicopter/holybro_x500v2_pixhawk6c)
* [https://docs.px4.io/main/assets/payloads_x500v2.BlKS32-f.png](https://docs.px4.io/main/assets/payloads_x500v2.BlKS32-f.png)
* [https://ntu-aris.github.io/ntu_viral_dataset/images/hardware.jpg](https://ntu-aris.github.io/ntu_viral_dataset/images/hardware.jpg)
* [https://docs.px4.io/main/assets/hero_image.DGHv_vvL.png](https://docs.px4.io/main/assets/hero_image.DGHv_vvL.png)


The Holybro design also helped me understand how professional development drones package their electronics.

---

## Learning

Before opening Fusion 360, I need to spend more time understanding drone design itself. There are still many things I don't fully understand, such as frame stiffness, vibration isolation, power distribution, ESC placement and battery mounting. I'll also look into Fusion 360 drone design tutorials and see how other people organize their CAD assemblies.

---

## Initial Design Decisions

The drone will be a **10-inch X-configuration quadcopter**. I chose the X layout since it is the standard for autonomous drones and provides symmetrical flight characteristics. It will use a **Pixhawk 6X with the Holybro Jetson Baseboard**, meaning the flight controller and companion computer are designed to work together as one stack.

My goal isn't racing or flying through goggles—it's an autonomous robotics platform. If I use a depth camera such as an Intel RealSense or Luxonis OAK-D, I already get an RGB camera together with depth sensing, so I probably won't need a separate forward-facing camera unless I specifically decide to add an FPV system later.

The drone will also include a GPS, RC receiver, telemetry radio and probably a VTX, although I'm still deciding whether the latter is actually necessary.

---

## Mechanical Analysis

Before committing to the frame dimensions I want to perform at least some simple engineering calculations instead of relying purely on intuition.

The first will be a basic stress analysis on the arms to estimate whether the chosen carbon fiber thickness is sufficient. The second will be a simple drop test calculation to get an idea of the loads during rough landings or crashes. These won't be full finite element simulations, but they should provide enough confidence before manufacturing.

References:

[https://sites.bu.edu/uav/files/2017/11/Frames.pdf](https://sites.bu.edu/uav/files/2017/11/Frames.pdf)

[https://blog.uavmodel.com/how-to-design-and-3d-print-custom-drone-frames/](https://blog.uavmodel.com/how-to-design-and-3d-print-custom-drone-frames/)

---

## Material Selection

At the moment, carbon fiber is still the obvious choice. It offers the best stiffness-to-weight ratio and is the standard material used in almost every modern drone frame.

I probably won't cut the first prototype directly from carbon fiber though. A better workflow would be to prototype using cheaper materials first, verify that everything fits together and only then manufacture the final version from carbon fiber.

---

## Notes and Decisions

A standard **10-inch propeller has a diameter of 254 mm**, which gives a good starting point for estimating the wheelbase.

One thing I underestimated was the size of the onboard computer. While the Jetson module itself isn't huge, the complete **Pixhawk 6X + Holybro Jetson Baseboard + Orin NX with heatsink** measures approximately **126 × 80 × 39–45 mm**. That assembly alone almost determines the minimum size of the center frame.

After comparing different options, I decided to use **four separate ESCs** instead of a single 4-in-1 ESC. A 4-in-1 board would simplify wiring and save some weight, but separate ESCs are easier to replace if one fails, distribute heat better and seem more appropriate for a research platform where reliability is more important than saving a few grams. This also means the frame will need a dedicated power distribution board.

I also decided that the **arms should be sandwiched between the upper and lower carbon plates**. This is the strongest configuration, makes replacing an arm straightforward and is widely used on larger carbon fiber frames.

The components that actually generate significant electrical interference are the ESCs, switching regulators and high-current battery wiring, not the Jetson itself.

The current frame concept is a two-level design. The Jetson Baseboard, telemetry and receiver will be mounted on the upper deck, while the lower section will contain the power distribution board and four ESCs. The battery will be mounted underneath the frame to keep the top free for electronics, and the depth camera will sit at the very front. The GPS will most likely be placed on a mast at the rear to minimize interference.

![Design 1](<Images/Screenshot 2026-08-05 091354.png>)

At this point, I expect many of these decisions to change. Right now the goal isn't to create the perfect drone, but to make enough informed decisions that I can finally start modeling something in Fusion 360 instead of endlessly researching. I already have a feeling I'll end up redesigning large parts of the frame once I start fitting the real components together.




--------
Drone General Design : Part 2 https://lapse.hackclub.com/timelapse/HdxbJGZdj3zA

![Design 2](<Images/Screenshot 2026-08-05 150327.png>)

After doing more research on the required hardware, I created a second design concept and started placing the major components inside the frame at approximately their real dimensions. The goal wasn't to create an accurate CAD model yet, but rather to check whether everything could realistically fit inside the central body before starting the detailed design in Fusion 360.

The battery remains mounted underneath the frame, while the upper section is reserved for the Pixhawk 6X with the Jetson Baseboard, the IP radio, RC receiver, GPS/compass and other electronics. I also decided to use four separate ESCs instead of a single 4-in-1 ESC, placing them closer to the arms to reduce motor wire length and make them easier to replace.

The Pixhawk and Jetson assembly is significantly larger than I initially expected, meaning the center frame will likely need to be larger than originally planned. It also became clear that cable routing, cooling and access for maintenance will be just as important as simply making all the components fit.

Overall, Design 2 feels much closer to a realistic research UAV than my original sketch. There is still plenty to redesign, but I now have a much better understanding of the internal layout and can begin translating this concept into a proper Fusion 360 assembly.

![Design 1 and Design 2 side by side](<Images/Screenshot 2026-08-05 150440.png>)

TODO : Wiring 

-----------
## Day 2


Drone General Design : Part 3 https://lapse.hackclub.com/timelapse/EFwJGuFalmob

Drone General Design : Part 4 : KiCAD Symbols https://lapse.hackclub.com/timelapse/CfTy0n8EebXS

Drone General Design : Part 5 : Routing and Components https://lapse.hackclub.com/timelapse/v2zys5-Etka2


Today I spent most of the time figuring out the electronics and communication architecture. I started by researching whether it would be better to use telemetry radios or switch to a 4G/5G solution. After looking into different options, I decided to move towards 4G/5G communication.

Afterwards, I created the initial BOM with all of the major components I plan to use. While doing wiring and other setup I ended up replacing and updating several components as I found options that fit the project better.

The next big task was preparing the project for KiCad. Instead of creating detailed symbols exposing every individual pin, I made simplified symbols that only expose the high-level connectors. Since my goal at this stage is to understand the overall architecture and wiring rather than design custom electronics, this approach keeps the schematic much cleaner and easier to read.

![All new elements](<Images/Screenshot 2026-08-06 212505.png>)

I also spent quite a bit of time figuring the Pixhawk Jetson Baseboard's connectors and ports and how everything is actually connected. 

Reference:
[https://docs.px4.io/main/assets/power1_one_battery_3s_4s.BwKdxwes.jpg](https://docs.px4.io/main/assets/power1_one_battery_3s_4s.BwKdxwes.jpg)

After that I updated the drone layout once again, resulting in what is currently my third design iteration. The overall placement of the components now feels much more realistic and is based on the actual hardware dimensions rather than rough estimates.

### Design Version 3

![Design Version 3](<Images/Screenshot 2026-08-07 012809.png>)

Finally, I created the first version of the complete system schematic in KiCad. It is intentionally kept at a high level, showing how the main subsystems connect together without going into individual signals or PCB-level details. 

### Schematics V1

![Schematics V1](<Images/Screenshot 2026-08-07 012645.png>)

There is still some uncertainty around some connector choices and communication hardware, so I expect that the schematic moght change over the next few days. Overall, I am satisfied with the results. One might argue it was unessesaary, but it is like trying to find buried treasures by memory or by map - both options have rights to exist, but one is obviously baeeter and faster in perspective even if initially, you spend some time on drawing the map, or n my case - creating the schematics.



-----
Day 3

Design V3.2

I already have the connections I want in KiCad, so now I started placing the connectors in their approximate physical locations on the board to see if everything will actually align and fit together eventually.

Shaped the props, ESCs and finally the motors. Done with all the main changes to the hardware components.

Now onto downloading the components' 3D models (or at least whatever I can find) and starting the actual design in Fusion.

Tnx GrabCAD, no copyright 💀
Some models are +- previews and not ideal, but close enough for now. All rights to their owners.

Found everything except the 5G module, so pretty satisfied. The model is getting pretty heavy though, and my laptop is struggling, so I might need to optimize everything before going too far.