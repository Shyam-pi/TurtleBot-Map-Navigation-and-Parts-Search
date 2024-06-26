cmake_minimum_required(VERSION 3.8)
project(group7_final)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(mage_msgs REQUIRED)
find_package(nav_msgs REQUIRED)
find_package(nav2_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(tf2_ros REQUIRED)
find_package(tf2 REQUIRED)
find_package(tf2_geometry_msgs REQUIRED)
find_package(ros2_aruco_interfaces REQUIRED)

add_executable(runner src/runner.cpp)
# add_executable(transform src/transform.cpp)
# add_executable(InitialPoseSetter src/InitialPoseSetter.cpp)

target_include_directories(runner PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>)

# target_include_directories(transform PUBLIC
#   $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
#   $<INSTALL_INTERFACE:include>)

# target_include_directories(InitialPoseSetter PUBLIC
#   $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
#   $<INSTALL_INTERFACE:include>)

target_compile_features(runner PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17
# target_compile_features(transform PUBLIC c_std_99 cxx_std_17)  # Require C99 and C++17

ament_target_dependencies(
  runner
  "rclcpp"
  "mage_msgs"
  "geometry_msgs"
  "std_msgs"
  "nav_msgs"
  "nav2_msgs"
  "tf2_ros"
  "tf2"
  "tf2_geometry_msgs"
  ros2_aruco_interfaces
)

# ament_target_dependencies(
#   transform
#   "rclcpp"
#   "mage_msgs"
#   "geometry_msgs"
#   "std_msgs"
#   "nav_msgs"
#   "nav2_msgs"
#   "tf2_ros"
#   "tf2"
#   "tf2_geometry_msgs"
#   ros2_aruco_interfaces
# )

# ament_target_dependencies(
#   InitialPoseSetter
#   "rclcpp"
#   "mage_msgs"
#   "geometry_msgs"
#   "std_msgs"
#   "nav_msgs"
#   "nav2_msgs"
#   "tf2_ros"
#   "tf2"
#   "tf2_geometry_msgs"
#   ros2_aruco_interfaces
# )

install(DIRECTORY include/
  DESTINATION include
)

install(TARGETS runner
  DESTINATION lib/${PROJECT_NAME})

# install(TARGETS transform
#   DESTINATION lib/${PROJECT_NAME})

# install(TARGETS InitialPoseSetter
#   DESTINATION lib/${PROJECT_NAME})

install(DIRECTORY config/ 
  DESTINATION share/${PROJECT_NAME}/config
)
install(DIRECTORY launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
