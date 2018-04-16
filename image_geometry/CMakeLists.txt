cmake_minimum_required(VERSION 3.5)

project(image_geometry)

find_package(ament_cmake REQUIRED)
find_package(OpenCV REQUIRED)
find_package(rclcpp REQUIRED)
find_package(sensor_msgs REQUIRED)

if(NOT CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra)
endif()

include_directories(
  include
  ${sensor_msgs_INCLUDE_DIRS}
  ${rclcpp_INCLUDE_DIRS})

if(NOT ANDROID)
  add_subdirectory(python)
endif()

add_subdirectory(src)

if(BUILD_TESTING)
  add_subdirectory(test)
endif()

ament_export_dependecies(OpenCV)

ament_export_include_directories(include)
ament_export_libraries(${PROJECT_NAME})

# add a library
add_library(
  ${PROJECT_NAME} 
  src/pinhole_camera_model.cpp 
  src/stereo_camera_model.cpp)

target_link_libraries(
  ${PROJECT_NAME} 
  ${OpenCV_LIBRARIES})

install(
  DIRECTORY include/${PROJECT_NAME}/
  DESTINATION include/${PROJECT_NAME}
)

ament_package()
