cmake_minimum_required(VERSION 2.8.3)
project(moveit_ikfast_simpler)

find_package(catkin REQUIRED COMPONENTS moveit_ikfast)

catkin_package()

foreach(f create_plugin gen_ikfast_cpp urdf2dae)
   install(PROGRAMS ${f} DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
endforeach(f)
