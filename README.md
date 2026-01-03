# DynaBARN

Repository for [DynaBARN](https://cs.gmu.edu/~xxiao2/Research/DynaBARN/DynaBARN.html). This code can be used to generate various DynaBARN environments of obstacles with different motion profiles. The 60 premade DynaBARN environments are at https://tufts.box.com/s/0dsoen9yno1qrnpj0l75eni7kmjdcx7c
The Gazebo world files are under the folder titled 'DynaBARN_worlds_60'. The plugin files are under 'all_cylinder_plugins'.
To simulate the 60 premade DynaBARN worlds, export the location of the plugins to the plugin path variable using 
```
export GAZEBO_PLUGIN_PATH=/path/to/plugins/testplugin/all_cylinder_plugins
```
Then simulate the environment using 
```
gazebo world_{world number}.world
```
## Example Worlds

![combined_big](https://user-images.githubusercontent.com/46573631/186241202-04005054-4157-46e2-b602-7565d62e8ba4.gif)


<!-- Easy World:


https://user-images.githubusercontent.com/46573631/185812166-b76cddd9-d2ca-4fd8-9a64-c41cc706c32e.mp4


Medium World:


https://user-images.githubusercontent.com/46573631/185812169-6a711fa1-8616-484b-a1df-7e8b1ccbf1d3.mp4


Hard World:


https://user-images.githubusercontent.com/46573631/185812175-7e8c0e44-5bd3-4981-8738-a84f4accdd21.mp4

 -->


## Requirements
> Most dependencies can be installed during the building of `the-barn-challenge-robo` except `matplotlib` & `scipy`. If you have built `the-barn-challenge-robo` following the installation guide, just do a `pip3 install matplotlib scipy`.
* Python
* NumPy
* Matplotlib
* SciPy
* cmake
* build-essential
* Ubuntu-18.04: Gazebo 9 & libgazebo9-dev
* Ubuntu-20.04: Gazebo 11 & libgazebo11-dev
 
## Using this repository
After cloning this repository onto your computer, create two folders called "plugins" and "worlds" in the same directory (optional). 
There are a few arguments for creating the trajectories and worlds:
* --save_dir and --plugin_dir are the directories for the world files and plugins, respectively
* --min_object and --max_object are the minimum and maximum number of obstacles in each world
* --n_worlds are the number of worlds to generate 
* --min_speed and --max_speed are the minimum and maximum speeds between each waypoint in the trajectories for each obstacle
* --min_std and --max_std are the minimum and maximum standard deviations in speed between each waypoint
* --difficulty is the difficulty to label each trajectory, but it is not necessary

Generate worlds & plugins
```
python3 create_plugin_polynomial.py --n_worlds 5 --min_speed 0.5 --max_speed 2.0 --min_std 0.1 --max_std 0.2 --min_order 1 --max_order 4
```
Run generated world
```
export GAZEBO_PLUGIN_PATH=/path/to/DynaBARN/plugins/build:${GAZEBO_PLUGIN_PATH}
cd /path/to/DynaBARN/worlds
gazebo --verbose world_0.world
```

> ⚠️ NOTE: `n_worlds` & `difficulty` arguments are not in used. Current `create_plugin_polynomial.py` is hardcoded to always generate 20 worlds and 200 plugins. Second run of that script will overwrite previous generation unless `save_dir` and `plugin_dir` is set differently.
