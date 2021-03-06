if (NOT DEFINED TEST_PROJECT_NAME)
    set (TEST_PROJECT_NAME "PigBusTest")
endif()

if (BUILD_TESTING_STANDALONE)
    add_executable(${TEST_PROJECT_NAME} "")
	target_link_libraries(${TEST_PROJECT_NAME} gmock_main ${PROJECT_NAME})
	set_target_properties(${TEST_PROJECT_NAME} PROPERTIES COMPILE_FLAGS "/FS" LINK_FLAGS "")
	include_directories(${PROJECT_BINARY_DIR}/googletest-src/googlemock/include/gmock)
	include_directories(${PROJECT_BINARY_DIR}/googletest-src/googletest/include/gtest)

    # Download and unpack googletest at configure time
    configure_file(CMakeLists.txt.in googletest-download/CMakeLists.txt)
    execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
      RESULT_VARIABLE result
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
    if(result)
      message(FATAL_ERROR "CMake step for googletest failed: ${result}")
    endif()
    execute_process(COMMAND ${CMAKE_COMMAND} --build .
      RESULT_VARIABLE result
      WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/googletest-download )
    if(result)
      message(FATAL_ERROR "Build step for googletest failed: ${result}")
    endif()

    # Prevent overriding the parent project's compiler/linker
    # settings on Windows
    set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

    # Add googletest directly to our build. This defines
    # the gtest and gtest_main targets.
    add_subdirectory(${CMAKE_CURRENT_BINARY_DIR}/googletest-src
                     ${CMAKE_CURRENT_BINARY_DIR}/googletest-build
                     EXCLUDE_FROM_ALL)

    # The gtest/gtest_main targets carry header search path
    # dependencies automatically when using CMake 2.8.11 or
    # later. Otherwise we have to add them here ourselves.
    if (CMAKE_VERSION VERSION_LESS 2.8.11)
      include_directories("${gtest_SOURCE_DIR}/include")
    endif()
	
endif()

target_sources(${TEST_PROJECT_NAME} PRIVATE
${CMAKE_CURRENT_SOURCE_DIR}/Source/PigBusTest.cpp
)

target_include_directories(${TEST_PROJECT_NAME} PUBLIC
${CMAKE_CURRENT_SOURCE_DIR}/Include
)
