# fully_actuated_quadrotor
Support files to implement in both, simulation and real experiments, our proposed fully-actuated quadrotor with flaps. Tested simualtions and experiments were perform in the firmware version 1.12.0-rc1 of the main PX4-Firmware git-hub.

Before replacing or modify any file of the original firmware, it is suggested to build the firware for SITL simulation, this will create the rewquired files before being modied.


## Configuring the SITL simulation files

### Replace the files

In iris model's folder, replace the sdf file of this repositoy, unzip and paste the stl quad-rotor model into the meshes folder. This will replace the common iris quad-rotor into our proposed flap quad-rotor.

### Adding the modified plug-ins for the SITL simulation

In order to perform the simulations of out quad-rotor model, it is necessary to add the modified plug-ins in the src folder of the sitl-simulation files. For this, paste the file "gazebo_motor_model_alex.cpp" into the next direction "/tools/sitl_gazebo/src". And replace the "gazebo_motor_model.h" in the "/tools/sitl_gazebo/include". 

Make sure that, when paste or replace the files, open both files and make any non significative change and then save the file. This will help the compiler to know that some files were modified and need to be recompiled. 

Finally, replace the CMakeLists.txt file in the folder "/tools/sitl_gazebo/", or manually add the next two lines in the the respective files section
 add_library(gazebo_motor_model_alex SHARED src/gazebo_motor_model_alex.cpp)
 
and
 
 gazebo_motor_model_alex 
 

## PX4 flight controller firmware modifications

To modify the main flight controller firmware it is only required to merge the mc_rate_control and the mc_att_control foldes with the original folder located at "src/modules/". And the folder MultirotorMixer locsted at "src/lib/mixer/". Again, make sure to make a non significative change and save to make the compiler to consider the files changes.


