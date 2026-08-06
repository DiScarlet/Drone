Pixhawk6c size: https://docs.holybro.com/autopilot/pixhawk-6c/dimensions
Link to the board where i drew the concept : https://app.idroo.com/boards/iBzdX5M0Z2
Sample wiring: https://docs.px4.io/main/assets/pixhawk6x_wiring_diagram.BTILi51L.png

BEFORE START DONT FORGT for lidar ; XSHUT pins (recommended)

The VL53L1X has an XSHUT (shutdown) pin.

At startup:

Hold sensors 2 and 3 in reset.
Initialize sensor 1 and change its I²C address.
Release sensor 2, initialize it, assign a new address.
Release sensor 3, initialize it, assign a new address.

This is the method recommended by ST.