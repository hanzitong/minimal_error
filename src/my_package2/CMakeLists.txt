
cmake_minimum_required(VERSION 3.8)
project(my_package2)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(my_package1 REQUIRED)

# include_directories(
#   ${my_package1_INCLUDE_DIRS}
# )

add_executable(node_defdef src/node.cpp)
ament_target_dependencies(
  node_defdef
  rclcpp
  std_msgs
  my_package1
)

install(TARGETS
  node_defdef
  DESTINATION lib/${PROJECT_NAME}
  DESTINATION lib
)

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


