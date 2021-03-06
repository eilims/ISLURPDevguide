## Quadrotor Summary

This page covers the setup process for Quadrotor UAVs. Quadrotors have 4 propellers and two onboard computers, the Nvidia Jetson TK1 and the Pixhawk Flight Controller. The Nvidia Jetson TK1 is mostly responsible for managing motion tracking data of the vehicle and the Pixhawk is responsible for using sensors and controlling the vehicle. The quadcopters use OptiTrack motion tracking cameras for positioning during indoor missions and GPS for positioning during outdoor missions.

## Companion Computer Setup

![](/assets/Jetson-TK1_500.png)

**Companion Computer Nvidia Jetson TK1 Specifications:**

* CPU: Quad-Core Arm Cortex A15
* 2 GB x16 Memory with 64-bit Width
* 16 GB 4.51 eMMC Memory
* 1 Full-Size HDMI Port
* 1 USB 3.0 Port, A

_See more at \_\__\[\_Nvidia's Website_\]\([http:\/\/www.nvidia.com\/object\/jetson-tk1-embedded-dev-kit.html](http://www.nvidia.com/object/jetson-tk1-embedded-dev-kit.html)\)

#### Connecting the Jetson TK1 to the Pixhawk

1. The first step is to create a serial connection between the Pixhawk and the Jetson TK1. For this, we can use an FTDI cable with some modification to connect the _Telem 2_ port on the Pixhawk to the _USB_ port on the Jetson. Figure 1 details the connection between these two ports.

![](/assets/Jetson_to_Pixhawk.png)

_Note: Ensure that the SYSID\_THISMAV parameter on the FCU firmware matches the tgt\_system in the launch file for running mavros. If the two do not agree, some topic will not be published and\/or mavros will not work properly._

## Tuning Parameters

Testing with a live vehicle introduces a lot of sensor noise and therefore more drift. This can be alleviated to a certain extent by tuning the vehicle properly. On the PX4 flight stack, the following parameters should be tuned carefully:

* LNDMC\_THR\_MAX: Multicopter max throttle
* MPC\_Z\_VEL\_MAX: Maximum vertical velocity in AUTO mode and endpoint for stabilized modes \(ALTCTRL, POSCTRL\).
* [INAV\_W\_Z\_BARO](https://pixhawk.org/firmware/parameters#position_estimator_inav): Weight \(cutoff frequency\) for barometer altitude measurements.
* ATT\_EXT\_HDG\_M: Set to 2

It is also a good idea to properly trim the RC values so that the vehicle can hover without too much drift.

* RC Channel 3: Throttle
* RC Channel 4: Yaw \[Increase RC4\_TRIM to Yaw left\]
* RC Channel 1: Roll \[Increase RC1\_TRIM to Roll left\]
* RC Channel 2: Pitch \[Increase RC2\_TRIM to pitch forward\]

For Motive Tracker setup, ensure that the yaw is pointing in the right direction!! It is very important. Otherwise, you'll notice a lot of drifting behavior.

For details on working with GPS Coordinates, see [here](http://www.movable-type.co.uk/scripts/latlong.html).

