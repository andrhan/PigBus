add_library(PigBus STATIC
	PigBus.cpp
)

target_include_directories(PigBus PUBLIC
"${PROJECT_BINARY_DIR}" 
${CMAKE_CURRENT_SOURCE_DIR}/../Include
)
