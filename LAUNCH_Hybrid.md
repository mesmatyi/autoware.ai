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
cd autoware.ai_bleeding/
source install/setup.bash
roslaunch waypoint_planner astar_avoid_with_all.launch
```