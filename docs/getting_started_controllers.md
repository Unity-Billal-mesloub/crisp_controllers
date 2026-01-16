# Getting started with the ROS2 side

On the ROS2 side, we want to:
1. We want to run a low-level C++ [CRISP](https://github.com/utiasDSL/crisp_controllers) controller in your manipulator.
    The computer running the CRISP controller might need a real-time patch for the controller to run smoothly and safely. 
    You can check out the [Franka Robotics guide on how to set up a RT-patch.](https://frankarobotics.github.io/docs/installation_linux.html#setting-up-the-real-time-kernel)
    On newer Ubuntu versions, you can use [Ubuntu Pro](https://ubuntu.com/real-time) for an easy setup.
2. Start nodes for the cameras, the grippers and other sensors.

For both we provide container demos of robots test that are ready to use as well as for cameras, grippers and other sensors.

## Docker Container Demos 

For now, these are the available demos in this repository. New demos are welcome, in particular if tested with real hardware.
Some other manipulators that could be added to this list is [Duatic](https://github.com/Duatic/dynaarm_driver), Universal Robots or other dual setups.

| Robots | Franka Robotics FR3 | FR Dual FR3 | IIWA 14 | Kinova Gen3 |
| :--- | :---: | :---: | :---: | :---: |
| MuJoCo simulated Hardware | ✅ | ✅ | ✅ | ✅ |
| Real Hardware | ✅ | ✅ | ❔[^1]  | ❔[^1] |

[^1]: Untested, but effort interface available.

We also have some examples with cameras.

| Robots | Real Sense | Any Camera / Webcam | Orbecc |
| :--- | :---: | :---: | :---: |
| Camera demo | ✅ | ✅ |  ✅[^2] | 

[^2]: Available container at: https://github.com/danielsanjosepro/orbec_container_ros2


## Pixi container demos

Robots:
- FR3: https://github.com/danielsanjosepro/pixi_franka_ros2
- FER: https://github.com/danielsanjosepro/orbec_container_ros2

Cameras:
- usb_cam: https://github.com/danielsanjosepro/pixi_usbcam_ros2

Sensors:
- Anyskin: https://github.com/danielsanjosepro/anyskin_ros2
