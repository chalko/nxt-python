# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
# Load catkin and all dependencies required for this package
find_package(catkin )

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE RelWithDebInfo)


#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)


include(ExternalProject)

ExternalProject_Add( nxt_python_src
  PREFIX nxt_python_src
  GIT_REPOSITORY https://github.com/chalko/nxt-python.git
  GIT_TAG mine
  CONFIGURE_COMMAND ""
  BUILD_IN_SOURCE 1
  BUILD_COMMAND "" 
  INSTALL_COMMAND python setup.py build  --build-base /home/nick/dev/nxt_ws/build/nxt/nxt_python install --install-layout=deb --prefix=/home/nick/dev/nxt_ws/install --install-scripts=/home/nick/dev/nxt_ws/install/bin
)


project(nxt_python)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS rospy python-usb python-bluez unzip nxt_python_src
    CATKIN_DEPENDS # TODO
    INCLUDE_DIRS # TODO include
    LIBRARIES nxt_python_src # TODO
)

#catkin_python_setup()

#install(PROGRAMS scripts/myscript
#  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
