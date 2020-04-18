# panda_simulation

![Panda in Gazebo](assets/panda-in-gazebo.png?raw=true "Panda in Gazebo")

This package was written for ROS kinetic running under Ubuntu 16.04. Run the following commands to make sure that all additional packages are installed:

```
mkdir -p catkin_ws/src
cd catkin_ws/src
git clone https://github.com/TSE-26/panda_simulation
git clone https://github.com/TSE-26/panda_moveit_config
git clone https://github.com/TSE-26/franka_ros
cd ..
sudo apt-get install libboost-filesystem-dev
rosdep install --from-paths src --ignore-src -y --skip-keys libfranka
cd ..
```
It is also important that you build the *libfranka* library from source and pass its directory to *catkin_make*  when building this ROS package as described in [this tutorial](https://frankaemika.github.io/docs/installation.html#building-from-source).

Currently it includes a controller parameter config file and a launch file to launch the [Gazebo](http://gazebosim.org) simulation environment and the Panda robot from FRANKA EMIKA in it with the necessary controllers.

Build the catkin workspace and run the simulation:
```
catkin_make -j4 -DCMAKE_BUILD_TYPE=Release -DFranka_DIR:PATH=/path/to/libfranka/build
source devel/setup.bash
roslaunch panda_simulation simulation.launch
```

Depending on your operating systems language you might need to export the numeric type so that rviz can read the floating point numbers in the robot model correctly:

```
export LC_NUMERIC="en_US.UTF-8"
```
Otherwise, the robot will appear in rviz in a collapsed state.


You can see the full explanation on his [blog post](https://erdalpekel.de/?p=55).

