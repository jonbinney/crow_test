cmake_minimum_required(VERSION 2.8.3)
project(crow_test)

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

find_package(Boost REQUIRED COMPONENTS system thread)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES crow_test
#  CATKIN_DEPENDS roscpp
#  DEPENDS system_lib
)

include_directories(
  crow
  crow/http-parser
  ${catkin_INCLUDE_DIRS}
)

# Build http-parserlib
add_library(http-parser crow/http-parser/http_parser.c)

## Declare a cpp executable
add_executable(crow_test_node src/crow_test_node.cpp)
set_target_properties(crow_test_node PROPERTIES COMPILE_FLAGS -std=c++11)
target_link_libraries(crow_test_node http-parser ${catkin_LIBRARIES} ${Boost_LIBRARIES})

## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(crow_test_node crow_test_generate_messages_cpp)


#############
## Install ##
#############

# all install targets should use catkin DESTINATION variables
# See http://ros.org/doc/api/catkin/html/adv_user_guide/variables.html

## Mark executable scripts (Python etc.) for installation
## in contrast to setup.py, you can choose the destination
# install(PROGRAMS
#   scripts/my_python_script
#   DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark executables and/or libraries for installation
# install(TARGETS crow_test crow_test_node
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
# )

## Mark cpp header files for installation
# install(DIRECTORY include/${PROJECT_NAME}/
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

## Mark other files for installation (e.g. launch and bag files, etc.)
# install(FILES
#   # myfile1
#   # myfile2
#   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
# )

#############
## Testing ##
#############

## Add gtest based cpp test target and link libraries
# catkin_add_gtest(${PROJECT_NAME}-test test/test_crow_test.cpp)
# if(TARGET ${PROJECT_NAME}-test)
#   target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME})
# endif()

## Add folders to be run by python nosetests
# catkin_add_nosetests(test)
