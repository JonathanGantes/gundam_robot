# gundam_robot
ROS packages for GUNDAM robots

![GUNDAM Gazebo Simulation](img/gundam_rx78_world.png)

How to visualize URDF model
===========================

To visualize URDF file in your rviz, you can use `display.launch` file.
```
$ roslaunch gundam_rx78_description display.launch
```

How to run gazebo simulation
============================

To run a gazebo dynamics simulation, you can start `gundam_rx78_world.launch`.

```
$ roslaunch gundam_rx78_gazebo gundam_rx78_world.launch
```

If the gazebo simulation GUI is launched, You must start `start` button on the bottom of the gazebo UI to start dynamics calculation.

To control joint angles, try a sample script.

```
$ rosrun gundam_rx78_control joint_trajectory_client_example.py
```

Note that currently, we have several limitation on this simulation, we only have position controller etc.

You can also find sample motion control files in the `gundam_rx78_control/sample` directory.

For Developers Only
===================

How to setup workspace
----------------------

We recommend you to use `wstool` to setup you workspace.

```
$ mkdir -p catkin_ws/src
$ cd  catkin_ws
$ wstool init src
$ wstool merge -t src https://raw.githubusercontent.com/gundam-global-challenge/gundam_robot/.gundam.rosinstall
$ wstool update -t src
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ rosdep install -y -r --from-paths src --ignore-src
$ catkin build
$ source devel/setup.bash
```

How to install mesh and urdf file
---------------------------------

The Gundam URDF file is automatically generated from Collada DAE file.

First, download the Gundam Collada file (ex. `GGC_TestModel_rx78_20170112.DAE`) under `gundam_rx78_description` directory.
Then, run `./scripts/dae_to_urdf.py` file with the downloaded file name as an argument. This will create mesh files under `meshes/` directory and create the URDF file under `urdf/` directory.

Finally, rename the file name to `urdf/gundam_rx78.urdf`

```
$ roscd gundam_rx78_description
$ python ./scripts/ggc_dae_to_urdf.py GGC_TestModel_rx78_20170112.DAE
$ mv urdf/GGC_TestModel_rx78_20170112.urdf urdf/gundam_rx78.urdf
```