# Prepare for Hybrid A* launch

Pull && build modifications on the *MAIN_AGX*

```
cd ~/autoware.ai_bleeding/src/autoware/core_planning/
git pull
cd ~/autoware.ai_bleeding/
colcon build --continue-on-error
```
Optionally pull && build the nissan bringup package
```
cd ~/leaf_ws/src/nissan_leaf_ros
catkin build
``` 


## Options to launch the hybridA

### 1 Launch with simple script on the *MAIN_AGX*

```
./MAIN_AGX/back_up_hybrida.sh
```

### 2 Launch with launch files

Terminal 1
```
cd ~/autoware.ai
source install/setup.bash
roslaunch nissan_bringup euclidean_detect_MPC_follower.launch
```
Terminal 2
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
roslaunch waypoint_planner astar_avoid_with_all.launch
```

### 3 Launch from launch files and from the runtime manager

Terminal 1 with runtime manager 1.13
```
cd ~/autoware.ai
source install/setup.bash
rosrun runtime_manager runtime_manager_dialog.py
```
Terminal 2 with runtime manager 1.14+
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
rosrun runtime_manager runtime_manager_dialog.py
```
On runtime_manager 1.13

- On Computing tab click -> lidar_euclidean_cluster_detect
- On Computing tab click -> mpc_follwer

On runtime_manager 1.14+

- On Sensing tab click -> ray_ground_filter
- On Computing tab click -> costmap_generator


Terminal 3
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
roslaunch ll2_global_planner ll2_global_planner_node.launch
```
Terminal 4
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
roslaunch waypoint_maker waypoint_loader.launch
```
Terminal 5
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
rosrun waypoint_planner lane_pub.py
```
Terminal 6
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
roslaunch waypoint_planner astar_avoid.launch
```
Terminal 7
```
cd ~/autoware.ai_bleeding/
source install/setup.bash
roslaunch waypoint_planner velocity_set_lanelet2.launch
```