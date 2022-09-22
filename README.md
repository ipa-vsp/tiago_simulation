# tiago_simulation

```
cd docker
docker-compose up --build
```

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04

```
docker ps
docker exec -it <container-id> bash
```

`roslaunch tiago_gazebo tiago_gazebo.launch public_sim:=true end_effector:=pal-gripper` (inside container)

## Install ROS 2
https://docs.ros.org/en/galactic/Installation/Ubuntu-Install-Debians.html

## Next

`sudo apt install ros-galactic-ros1-bridge` (Requires ROS1 and ROS2)

Open new terminal

```
source /opt/ros/noetic/setup.bash 
source /opt/ros/galactic/setup.bash
ros2 run ros1_bridge dynamic_bridge
```

`ros2 topic pub /mobile_base_controller/cmd_vel  geometry_msgs/msg/Twist "{linear: {x: 2.0, y: 0.0, z: 0.0}, angular: {x: 0.0, y: 0.0, z: 1.8}}"`
