
cmake_minimum_required(VERSION 3.8)
project(my_package1)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

include_directories(include)

add_library(my_package1 SHARED
    src/my_func.cpp
)

target_include_directories(my_package1
    PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

# ament_export_dependencies(
#     rclcpp
#     ament_cmake
# )

ament_export_include_directories(   # without it , colcon cannot find xx.hpp
    include
)

ament_export_libraries( # without it , colcon cannot find src/xx.
    ${PROJECT_NAME}
)

install(TARGETS my_package1
    # EXPORT my_package1Targets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(DIRECTORY include/
    DESTINATION include
)


ament_package()
