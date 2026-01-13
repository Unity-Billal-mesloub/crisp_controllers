## 2. :snake: Use the python interface [CRISP_PY](https://github.com/utiasDSL/crisp_py) to control the robot

### Try it out with the robot

Make sure that the demo container is running in the background, as we will need it to access the robot.
From now on, you can instantiate `Robot` objects to control the robot.

??? example "Example robot usage:"
    ```py
    from crisp_py.robot import Robot
    from crisp_py.robot_config import RobotConfig

    robot_config = RobotConfig(...)
    robot = Robot(namespace="...", config=robot_config)  # (1)!
    robot.wait_until_ready()  # (2)!

    print(robot.end_effector_pose)


    robot.controller_switcher_client.switch_controller(
        "cartesian_impedance_controller",  # (4)!
    )  
    x, y, z = robot.end_effector_pose.position
    robot.set_target(position=[x, y, z-0.1])  # (3)!

    robot.shutdown()
    ```

    1. This will get information from the robot asynchronously
    2. Make sure that we get information from the robot before trying to set targets or reading the pose of the robot.
    3. Set target 10 cm downwards. Careful not to send poses that are too far away from the current one!
    4. This will request the controller manager to activate the cartesian impedance controller. You can use it with other controllers like the operational space controller!

## 3. Adding cameras, grippers, and further sensors to CRISP_PY


### Installation

!!! Note
    If you want to use the gymnasium interface, CRISP_PY will be automatically installed in the gym. You can therefore check the installation of [CRISP_GYM](#4-getting-started-with-crisp_gym) directly.
    However, this section still gives you an idea on how to use CRISP_PY with your robot. We do not recommend to skip it.

To use `CRISP_PY`, we recommend using [pixi](https://pixi.sh/latest/), a modern conda-like package manager.
It can be used in combination with [robostack](https://robostack.github.io/) to easily install ROS2 in any machine.
There are a few ways to get you started:

_... use in your already existing pixi project:_

To use `CRISP_PY` in an already existing pixi project, you need to make sure that `ROS2` is available.
Check the [pixi.toml](https://github.com/utiasDSL/crisp_py/blob/main/pixi.toml) of `CRISP_PY` to see how this looks like.
Then you can add `CRISP_PY` as a pypi package:
```bash
pixi add --pypi crisp-python
```
or
```bash
uv add crisp-python
```
or
```bash
pip install crisp-python
```
Double-check that everything is working by running:

```bash
python -c "import crisp_py"  # (1)!
```

1. This should not log anything if everything is fine

_... install from source:_

```bash
git clone https://github.com/utiasDSL/crisp_py
cd crisp_py
pixi install
pixi shell -e humble
python -c "import crisp_py"  # (1)!
```

1. This should not log anything if everything is fine

Now you can try to control the robot! Check out the [examples](https://github.com/utiasDSL/crisp_py/blob/main/examples) for inspiration.
