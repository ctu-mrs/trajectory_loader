# Tutorial for trajectory_loader of MRS ROS system

Launchfiles and config files are only examples how to use this package. It is recommended to copy launchfiles and config file into your own package and modify them there.

## Commanding single client machines

### Load trajectory into MPC tracker from CSV or SSV file

Loading is done by calling:
```bash
roslaunch trajectory_handler single_trajectory_from_file.launch current_working_directory:=<folder> file:=<file>
```
where parameters *<folder>* and *<file>* are parameters that have to be set. Furthermore, another parameters of the trajectory can be set by modifying the launch file:
* offset - offset for the whole trajectory [x,y,z,yaw].
* delay - sleep before loading the trajectory.
* use_yaw - set if the yaw controller should follow the predefined yaw angle in the trajectory.
* fly_now - set if the trajectory should be followed immediately after its loading. 
* loop - set if the trajectory is infinite. Trajectory will be then in the loop.

## Commanding multiple client machines

### Prerequisites 

Setting which UAVs are target and also which trajectories should be loaded is set in config file */config/params.yaml*.
All launch files are using parameter *uav_name_list*, that should be array of target UAVS.

### For simulations via LAN
Follow to [how to set ros remote](https://mrs.felk.cvut.cz/gitlab/uav/uav_core/wikis/ros_remote) page.

### For real UAV
To have correctly set multimaster net using package multimaster_fkie or nimbro_network. (Usually it is already prepared).

### Load trajectories into MPC tracker from CSV or SSV files

Loading is done by calling:
```bash
roslaunch trajectory_handler multimaster_trajectories_loader.launch
```
the parameters can be set similarly as for single client. Only parameter *delay* has to be set for each target UAV individually.

### Sending command "Fly to start"

```bash
roslaunch trajectory_handler multimaster_fly_to_start.launch
```

### Sending command "Start following"

```bash
roslaunch trajectory_handler multimaster_start_following.launch
```

