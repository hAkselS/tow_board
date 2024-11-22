
cmake_minimum_required(VERSION 3.8)
project(mouss_mini)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
# find dependencies
find_package(ament_cmake REQUIRED)
# needed for python builds
find_package(ament_cmake_python REQUIRED)
find_package(rclpy REQUIRED)
# required for adding custom services
find_package(rosidl_default_generators REQUIRED)
find_package(mouss_mini) # ISSUE LINE

# custome service stuff 
# set(srv_files
#   "srv/AddTwoInts.srv"
#   )
# set(srv_files
#   "srv/GetDropDir.srv"
# )

# set(msg_files
#   "msg/CameraData.msg"
#   "msg/SystemStatus.msg"
#   "msg/DepthTemp.msg"
# )

rosidl_generate_interfaces(${PROJECT_NAME}
  ${srv_files}
  ${msg_files}
  DEPENDENCIES ${interface_dependencies}
  ADD_LINTER_TESTS
)
ament_python_install_package(scripts)

# Install Python executables
install(PROGRAMS
  scripts/publisher.py
  scripts/subscriber.py
  DESTINATION lib/${PROJECT_NAME}
)

# Install launch files
# install(DIRECTORY
#   launch
#   DESTINATION share/${PROJECT_NAME}/
# )

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # comment the line when a copyright and license is added to all source files
  set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # comment the line when this package is in a git repo and when
  # a copyright and license is added to all source files
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
