cmake_minimum_required(VERSION 3.10)
project(eigen_conversions)

find_package(ament_cmake REQUIRED)
find_package(orocos_kdl REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(std_msgs REQUIRED)
find_package(Eigen3 REQUIRED)

include(GNUInstallDirs)

include_directories(include)

add_library(${PROJECT_NAME}
  src/eigen_msg.cpp
  src/eigen_kdl.cpp
)
ament_target_dependencies(${PROJECT_NAME} std_msgs geometry_msgs orocos_kdl Eigen3)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/${PROJECT_NAME})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
  RUNTIME DESTINATION ${CMAKE_INSTALL_LIBDIR})

ament_export_libraries(${PROJECT_NAME})
ament_export_dependencies(geometry_msgs std_msgs Eigen3 orocos_kdl)
ament_export_include_directories(include)
ament_package()
