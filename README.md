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

Note: the scripts in `moveit_ikfast` automatically update the
`kinematics.yaml` file in the relevant MoveIt config package.


## Steps

I find it easiest to do this in a workspace that overlays the workspace that
contains the urdfs and MoveIt configuration packages, but that is obviously
not needed.

This example below is for the Fanuc M-10iA model (found in the
`fanuc_m10ia_support` package). Update as needed.


 1. Create scratch directory (in the cwd):

  ```bash
  mkdir m10ia
  cd m10ia
  ```


 1. Convert urdf to Collada (in the scratch dir):

  ```bash
  rosrun moveit_ikfast_simpler urdf2dae \
    `rospack find fanuc_m10ia_support`/urdf/m10ia.urdf
  ```


 1. Generate IKFast solution, using Collada file (again, in the scratch dir):

  ```bash
  rosrun moveit_ikfast_simpler gen_ikfast_cpp m10ia.dae
  ```


 1. Create plugin package (in the scratch dir), using Collada file and
    generated IKFast source file:

  ```bash
  rosrun moveit_ikfast_simpler create_plugin \
    m10ia.dae \
    ikfast61_transform6d_fanuc_m10ia_manipulator.cpp
  ```

 1. Update manifest and move package to proper location


## Dependencies

 - python
 - openrave 0.8
 - sed, grep


## References

 1. http://wiki.ros.org/Industrial/Tutorials/Create_a_Fast_IK_Solution
 1. http://wiki.ros.org/Industrial/Tutorials/Create_a_Fast_IK_Solution/moveit_plugin
 1. http://moveit.ros.org/wiki/Kinematics/IKFast
 1. http://answers.ros.org/question/65940/difficulty-using-ikfast-generator-need-6-joints-error-with-kuka-youbot/
