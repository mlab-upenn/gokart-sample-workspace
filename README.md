# UPenn GoKart ROS 2 Sample Workspace

A ROS 2 Sample Workspace with the [UPenn GoKart Simulator][gokart-simulation].


## Development

**Requirements:**
* Ubuntu 20.04
* a working installation of ROS 2 Foxy (newer versions might work as well), see [Installing ROS 2 via Debian Packages][ros2-foxy-debian-pkgs]
* [vcstool](https://github.com/dirk-thomas/vcstool)
  * Test if you have it using: `vcs --version` (should print `vcs 0.3.0`)
  * You can install using `sudo apt install python3-vcstool` or `python3 -m pip install -U vcstool`


### Note about sourcing

**Note!** Always use a separate terminal windows/tabs for building and running.

In a terminal window/tab where you are building the workspace, you must source **only** the ROS 2 Foxy (`source /opt/ros/foxy.setup.bash`).

Then, in other terminal windows/tabs you can source the built workspace (`source install/setup.bash`) and run the programs.

If you source workspace in the building terminal window/tab, then you will pollute the environment and the resulting built workspace might not work correctly.


### First-time Setup

In the repo/workspace root, run:
```bash
source /opt/ros/foxy/setup.bash
vcs import < gokart.foxy.repos
./src/gokart/rosdep/install.sh
rosdep install -i --from-paths src -y
```

`./src/gokart/rosdep/install.sh` installs custom rosdep lists file. This needs to be done only once.
See [gokart-rosdep].


### Run when you pull the latest changes

Re-run `vcs` and `rosdep` when you pull the latest changes:
```bash
source /opt/ros/foxy/setup.bash
vcs import < gokart.foxy.repos
vcs pull < gokart.foxy.repos
rosdep install -i --from-paths src -y
```


### Building

Use a building terminal window/tab:
```bash
source /opt/ros/foxy/setup.bash
colcon build --packages-up-to simulator
```


### Run the simulation

Use a running terminal window/tab:
```bash
source install/setup.bash
ros2 launch simulator simulation.launch.py teleop:=key
```

See [gokart-simulation/simulator] for more all options.


<!-- links references -->

[ev-grand-prix-autonomous]: https://evgrandprix.org/autonomous/

[ros2-foxy-debian-pkgs]: https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html

[gokart-rosdep]: https://github.com/mlab-upenn/gokart-rosdep

[gokart-simulation]: https://github.com/mlab-upenn/gokart-simulation

[gokart-simulation/simulator]: https://github.com/mlab-upenn/gokart-simulation/tree/main/simulator
