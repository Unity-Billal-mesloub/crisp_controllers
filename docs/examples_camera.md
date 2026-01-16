# Camera Examples

### Cameras

The cameras that we tested are:

- Any usb camera or webcam using the [ROS2 usb-cam](https://github.com/ros-drivers/usb_cam) package,
- [Real Sense](https://github.com/IntelRealSense/realsense-ros/tree/ros2-master) which gives amazing ROS2 support,
- and [Orbbec](https://github.com/orbbec/OrbbecSDK_ROS2).

Check the [getting ros2 side ready guide](getting_started_controllers.md) to see some examples with cameras

??? example "Example camera usage:"
    ```py
    import cv2
    from crisp_py.camera import Camera, CameraConfig

    camera_config = CameraConfig(
        camera_name="primary",
        resolution=(256, 256),  # (1)!
        camera_color_image_topic="image_raw",  # (2)!
        camera_color_info_topic="camera_info",
    )

    camera = Camera(config=camera_config)  # (3)!
    camera.wait_until_ready() # (4)!

    cv2.imshow("Camera Image", camera.current_image)  # (5)!
    cv2.waitKey(0)

    ```

    1. You can define a custom resolution, independently of the resolution of the published image.
    2. Set here the topic of your custom camera name. crisp_py uses compressed images, so make sure that this topic is available as well.
    3. You can also pass `namespace="..."` to give the camera a namespace. This is required for a bimanual setup.
    4. Make sure that we received an image. This will fail with a timeout if the topic is wrong or the camera is not publishing.
    5. This will show you the latest received image!

## Run a camera with `pixi/robostack`
Here is an example of setting up and running the `usb_cam` ROS2 node using `pixi` and `robostack`.
The USB camera that you use could be your laptop webcam or an external USB camera connected to your computer.
First, create a folder `mkdir pixi_usb_cam, cd pixi_usb_cam` and create a `pixi.toml` file with the following content:

```toml title="pixi.toml"
[workspace]
authors = ["Your Name <your-email@domain.com>"]
channels = ["conda-forge"]
name = "test_usb_cam"
platforms = ["linux-64"]
version = "1.1.0"

[dependencies]
python = "*"
cmake = "*"
poco = "*"
libpsl = "*"

[target.linux.dependencies]
libgl-devel = "*"

[environments]
# humble = { features = ["humble"] }
jazzy = { features = ["jazzy"] }

[feature.jazzy]
channels = ["https://prefix.dev/robostack-jazzy"]

[feature.jazzy.dependencies]
ros-jazzy-desktop = "*"
ros-jazzy-image-transport = "*"
ros-jazzy-image-transport-plugins = "*"
colcon-common-extensions = "*"
ros-jazzy-usb-cam = "*"

[feature.jazzy.tasks]
usb_cam = "ros2 run usb_cam usb_cam_node_exe"
```

Then in a terminal to start the `usb_cam` node run:
```bash
pixi run usb_cam
```

Now camera images are being published. In a different terminal, you can run:
```bash
pixi shell -e jazzy
ros2 topic list
# rqt to also visualize the image
```

## Access images from `crisp_py`

Using the Camera class from `crisp_py`:
```python
"""Simple example showing how to use the Camera class to capture and display an image."""

import cv2
from crisp_py.camera import Camera, CameraConfig

camera_config = CameraConfig(
    camera_name="primary",
    camera_frame="primary_link",
    resolution=(256, 256),
    camera_color_image_topic="/camera_namespace/wrist_camera/color/image_rect_raw",
    camera_color_info_topic="/camera_namespace/wrist_camera/color/camera_info",
)

camera = Camera(config=camera_config, namespace="")
camera.wait_until_ready()

cv2.imshow("Camera Image", camera.current_image)
cv2.waitKey(0)
```

Or by defining a camera in a YAML configuration file:
```yaml
camera_name: "primary"
camera_frame: "primary_link"
resolution: [256, 256]
camera_color_image_topic: "/camera_namespace/wrist_camera/color/image_rect_raw"
camera_color_info_topic: "/camera_namespace/wrist_camera/color/camera_info"
```

Then load the configuration and use the Camera class:

```python
"""Example showing how to load camera configuration from a YAML file."""
import cv2
from crisp_py.camera import make_camera

camera = make_camera("your_config_file_name")
camera.wait_until_ready()

cv2.imshow("Camera Image", camera.current_image)
cv2.waitKey(0)
```


