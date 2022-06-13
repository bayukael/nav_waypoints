# nav_waypoints
## Description
A simple package to send several `move_base` goals from a given csv file sequentially.

This package does not depend on `turtlebot3_simulation` and navigation packages although there are several `launch` files which runs some navigation packages (`move_base` and `amcl`) and some turtlebot3 packages. These launch files are provided to make it easy to try this package. The same arguments also apply to folder `param`, `maps`, and `rviz`.

There is also docker compose file which is designated to run `nav_waypoint` package on the docker while the simulation is run on the host.

## Usage
1. Create a catkin workspace and navigate to folder `src`.
```bash
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
```
2. Copy `turtlebot3_simulation` package and `nav_waypoints` package the workspace
```bash
git clone -b noetic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cp -r path/to/dir/nav_waypoints ~/catkin_ws/src
```
3. Build and source the workspace
```bash
cd ~/catkin_ws && catkin_make
source ~/catkin_ws/devel/setup.bash
```
4. Run the simulation. This command will open gazebo and rviz.
```bash
roslaunch nav_waypoints bayu_navigation.launch
```
5. Open the rviz and properly set the initial pose by using "2D Pose Estimate"

6. Navigate to `nav_waypoints` package and run docker-compose.
```bash
cd ~/catkin_ws/src/nav_waypoints
docker compose up
```
7. You should see the robot follows a series of waypoints which has been defined in `nav_waypoints/data/waypoints.csv`.
8. After the robot finishes all the waypoints, the docker container should stop by itself. If it is not, please Ctrl+C. Then proceed with removing the container
```bash
docker compose down
```
## Customization
The example above uses file `waypoints.csv` that resides in folder `nav_waypoints/data`. To create other set of waypoints, this `waypoints.csv` must be edited. Note that the file consists of four columns: `x, y, w, z`. Please make sure that the waypoints inserted into the `waypoints.csv` corresponds to the map used in the simulation.
