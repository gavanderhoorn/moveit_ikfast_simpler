cmake_minimum_required(VERSION 2.8.3)
project(moveit_ikfast_simpler)

find_package(catkin REQUIRED)

catkin_package()

install(PROGRAMS create_plugin gen_ikfast_cpp urdf2dae
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
