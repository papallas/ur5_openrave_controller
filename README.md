# UR5 Controller for OpenRAVE
This controller will listen to ROS topic that publishes the joints of UR5 in real time. Will allow visualising the current state
of a UR5 in OpenRAVE either from a real, physical, robot or through a simulation like MoveIt!.

## Includes
This repository includes the following:
- The custom written controller for OpenRAVE and UR5 robot.
- The URDF and SRDF files to load UR5 model into 

## How to install
The installation of this project requires some prerequisites. 

1. You need to install and configure another OpenRAVE plugin called `or_urdf` this plugin is available [here](https://github.com/personalrobotics/or_urdf)
I have written a blog post on how to install this plugin if you struggle to find a solution, find the tutorial [here]().
2. You need to install a dummy ROS OpenRAVE package that creates links for the OpenRAVE installation so ROS is aware of the
path of the OpenRAVE software. You can download and install this dummy package from [here]().
3. Once you install `or_urdf` you need to download the contents of this repository into a rosmake directory. This package uses a
rosmake instead of catkin_make. I suggest that you:
   - Create a new directory called `rosmake_ws` in your home directory.
   - Edit your `.bashrc` file located under your home directory: `gedit ~/.bashrc` and add the following line at the end of the file: `export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/rosmake_ws`
   - Clone this directory into `rosmake_ws`, it should be named `ur5controller`.
   - `cd` into the directory `ur5controller` and run `rosmake`. You should see a compile process taking place and at the end
   a message saying the successful builds and the failed ones. You should have 0 failed in which case everything works perfectly. If you do get failures review the error and try to solve the problem.
   - Edit once again your `.bashrc` file located under your home directory: `gedit ~/.bashrc` and add the following line at the end of the file: `export OPENRAVE_PLUGINS=$OPENRAVE_PLUGINS:~/rosmake_ws/ur5controller/lib`
   - Now you need to either close the current terminal or run `source ~/.bashrc`.
   - Verify that the controller is successfully installed by running `openrave --listplugins` you should see `URDF` under module and `Ur5Controller` under controllers.
4. Once everything is successful with the above process you need to generate the `.urdf` file. I have created a handy Python script that will make this process easy for you.
   - In `ur5controller` directory located in `rosmake_ws` you should have a directory called `ur5_model` and within this directory, you should have a Python file called `urdf_file_generator.py'.
     - Run the Python script `urdf_file_generator.py` and if you are happy having the meshes and the URDF and SRDF files under
     `~/rosmake_ws/ur5controller/ur5_model` then proceed and hit enter for the path you are required to provide as input. If however, you
     prefer having those files into a different location go ahead and move them into another directory and run the Python script
     within this new directory.
     - Once you run it a `ur5.urdf` file should be generated containing all the information needed with the hard-coded URI paths
     that the Python script have created for you.
