cmake_minimum_required(VERSION 3.5)
project(social_navigation_actions)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_BUILD_TYPE DEBUG)

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclcpp_action REQUIRED)
find_package(plansys2_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(diagnostic_msgs REQUIRED)
find_package(nav2_msgs REQUIRED)
find_package(plansys2_executor REQUIRED)
find_package(plansys2_domain_expert REQUIRED)


find_package(nav2_costmap_2d REQUIRED)
find_package(social_navigation_msgs REQUIRED)

set(dependencies
    rclcpp
    rclcpp_action
    plansys2_msgs
    nav2_msgs
    diagnostic_msgs
    plansys2_executor
    plansys2_domain_expert
    nav2_costmap_2d
    social_navigation_msgs
)

add_executable(escort_action_node src/escort_action_node.cpp)
ament_target_dependencies(escort_action_node ${dependencies})

add_executable(follow_action_node src/follow_action_node.cpp)
ament_target_dependencies(follow_action_node ${dependencies})

add_executable(approach_action_node src/approach_action_node.cpp)
ament_target_dependencies(approach_action_node ${dependencies})

add_executable(move_action_node src/move_action_node.cpp)
ament_target_dependencies(move_action_node ${dependencies})

add_executable(approach_controller_node src/controllers/approach_controller_node.cpp)
ament_target_dependencies(approach_controller_node ${dependencies})

add_executable(escort_controller_node src/controllers/escort_controller_node.cpp)
ament_target_dependencies(escort_controller_node ${dependencies})

add_executable(follow_controller_node src/controllers/follow_controller_node.cpp)
ament_target_dependencies(follow_controller_node ${dependencies})

install(DIRECTORY launch pddl DESTINATION share/${PROJECT_NAME})

install(TARGETS
  escort_action_node
  follow_action_node
  approach_action_node
  move_action_node
  approach_controller_node
  escort_controller_node
  follow_controller_node
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION lib/${PROJECT_NAME}
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()

  #find_package(ament_cmake_gtest REQUIRED)
endif()

ament_export_dependencies(${dependencies})

ament_package()