cmake_minimum_required(VERSION 3.10)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(BUILD_TESTING ON)
set(BUILD_TESTING_STANDALONE ON)
set(BUILD_SANDBOX ON)

set(PROJECT_NAME "PigBus")
set(TEST_PROJECT_NAME "PigBusTest")

if (BUILD_SANDBOX)
	project(${PROJECT_NAME} VERSION 1.0)
endif()

# Add libraries
add_subdirectory(Source)

if (BUILD_TESTING)
    add_subdirectory(Test)
endif()
