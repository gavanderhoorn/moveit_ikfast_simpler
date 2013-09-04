moveit_ikfast_simpler
=====================

This package contains a few scripts that wrap the scripts provided by the 
moveit_ikfast package. I found myself repeating the same steps every time I 
had to create an IKFast MoveIt plugin, so I created some simple convenience 
scripts.

There is a good chance this doesn't work for arbitrary URDFs: it is assumed 
that the URDFs contain only a single kinematic chain: from `base_link` to 
`tool0`. By default, this generates a `transform6d` plugin, so a maximum of 
6 DOF (actually a minimum as well, as `translationdirection5d` as an IKFast 
type hasn't worked for me yet).

Be aware that the scripts in `moveit_ikfast` automatically update the 
`kinematics.yaml` file in the relevant MoveIt config package.


## Steps

 1. Create collada DAE of URDF (in the cwd):

  ```bash
  rosrun moveit_ikfast_simpler urdf2dae /path/to/file.urdf
  ```


 1. Generate IKFast solution, using DAE (again, in the cwd):

  ```bash
  rosrun moveit_ikfast_simpler gen_ikfast_cpp /path/to/file.dae
  ```


 1. Create plugin package (in the cwd), using DAE and IKFast source:

  ```bash
  rosrun moveit_ikfast_simpler create_plugin /path/to/file.dae /path/to/ikfast.cpp
  ```

 1. Update manifest and move package to proper location


## References

 1. http://wiki.ros.org/Industrial/Tutorials/Create_a_Fast_IK_Solution
 1. http://wiki.ros.org/Industrial/Tutorials/Create_a_Fast_IK_Solution/moveit_plugin
 1. http://moveit.ros.org/wiki/Kinematics/IKFast
 1. http://answers.ros.org/question/65940/difficulty-using-ikfast-generator-need-6-joints-error-with-kuka-youbot/
