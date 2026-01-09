# Getting started with the ROS2 side

## Demos 

For now, these are the available demos in this repository. New demos are welcome, in particular if tested with real hardware.
Some other manipulators that could be added to this list is [Duatic](https://github.com/Duatic/dynaarm_driver) or other dual setups.

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


## Get the robot ready

Getting the low-level C++ [CRISP](https://github.com/utiasDSL/crisp_controllers) controller ready for your manipulator
The computer running the CRISP controller might need a real-time patch for the controller to run smoothly and safely. You can check out the [Franka Robotics guide on how to set up a RT-patch.](https://frankarobotics.github.io/docs/installation_linux.html#setting-up-the-real-time-kernel)
On newer Ubuntu versions, you can use [Ubuntu Pro](https://ubuntu.com/real-time) for an easy setup.

Then, check if your robot is already included in one of our demos, check [how to run a demo](misc/demos.md) from our [demos repository](https://github.com/utiasDSL/crisp_controllers_demos). You can then follow the instructions there to start your robot(s) using a Docker container. Some of them offer the possibility to run the demos with simulated robots to test the setup.

If your robot is not included in the demos that is not problem. Check out [How to set up a robot that is not available in the demos](misc/new_robot_setup.md). Once you get the controllers running, feel free to open a pull request on our repo to add it to the demos! We highly appreciate that!


## Get the cameras ready

pass

## Get the gripper ready

pass

## Get the sensors ready

pass
