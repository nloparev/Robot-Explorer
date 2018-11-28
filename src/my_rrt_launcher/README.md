### my_rrt_launcher
### 11/28/2018
Use [hector_slam](http://wiki.ros.org/hector_slam) for occupancy grid mappping using data collected using a [HOKUYO(URG-04LX-UG01)](https://www.hokuyo-aut.jp/search/single.php?serial=166) laser range finder Turtlebot. [Rapidly Exploring Random Tree RRT*   algorithm](http://paper.ijcsns.org/07_book/201610/20161004.pdf) was used for planning a path towards a goal determined by a service provider.

## Getting Started
1) download ```spain_a3```, ```rrt_exploration_tutorials``` at [https://github.com/hasauino/rrt_exploration_tutorials](https://github.com/hasauino/rrt_exploration_tutorials) and ```hector_slam``` at [https://github.com/tu-darmstadt-ros-pkg/hector_slam](https://github.com/tu-darmstadt-ros-pkg/hector_slam)
2) place in ```[catkin_ws]/src``` folder.
3) run catkin_make, followed by ```source devel setup.bash``` to build all packages within your ```catkin_ws``` and make your ```catkin_make``` visible.

## Running
**Part I (Hector SLAM):**
1) run: ```roslaunch spain_a3 my_hector_slam_turtlebot.launch```
2) In a new terminal run: ```rosbag play rosbags/assignment3_5floor.bag --clock```
To save the maps for safe keeping in the ```maps``` directory you can run: ```rosrun map_server map_saver -f ~/map/<map_name>```
3) End processes with cmd + C, and ```killall gzerver```


**Part II (RRT and goal pursuit):**
1) run: ```roslaunch spain_a3 find_goal_in_house.launch```
2) To use the RRT algorithm to navigate towards the default goal, open a new terminal and run: ```python fetch_goal.py```

## Testing
Once launched you can set the goal by modifying the position array in ```__main__``` the default position is:
```position = {'x': 1.36, 'y' : -1.46}```


## My Simple Server Summary
My server: ```fetch_goal.py``` communicates with action```robot_1/move_base```
and frame id: ```robot_1/map``` which corresponds to my map coordinate frame. This can be examined by running ```tf echo robot_1/map robot_1/move_base``` which will give you the transformation both linear and angular to go from the map frame to the base frame.

This was sourced from: [ROS](http://wiki.ros.org/navigation/Tutorials/SendingSimpleGoals)


-----------------------------------
## References
* RRT Algorithm: [github.com/hasauino](https://github.com/hasauino)
* Paper on RRT from [Hassan Umari et al.](https://ieeexplore.ieee.org/document/8202319)
* [Turtlebot Tutorials](http://learn.turtlebot.com)
