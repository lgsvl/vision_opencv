# add the tests
find_package(ament_cmake_gtest REQUIRED)

# add boost directories for now
include_directories("../src")

ament_add_gtest(${PROJECT_NAME}-utest test_endian.cpp test_compression.cpp utest.cpp utest2.cpp test_rgb_colors.cpp APPEND_LIBRARY_DIRS "${cv_bridge_lib_dir}")
target_link_libraries(${PROJECT_NAME}-utest
  ${PROJECT_NAME}
  ${OpenCV_LIBRARIES}
)

# TODO(gaoethan) Reenable this when tests are ported to ROS 2
# find_package(ament_cmake_pytest REQUIRED)
# ament_add_pytest_test(enumerants.py "enumerants.py")
# ament_add_pytest_test(conversions.py "conversions.py")
# ament_add_pytest_test(python_bindings.py "python_bindings.py")
