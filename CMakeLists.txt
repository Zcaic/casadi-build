cmake_minimum_required(VERSION 3.26)

project(cst)

# set(CMAKE_CXX_STANDARD 17)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
# set(CMAKE_CXX_EXTENSIONS OFF)

# add_subdirectory("./deps/casadi")

list(PREPEND CMAKE_PREFIX_PATH "/install/casadi/cmake")
find_package(casadi REQUIRED)
add_executable(test "./test/test.cpp")
set_target_properties(test PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/out)
target_link_libraries(test PRIVATE casadi)
file(GLOB copy_files ${CMAKE_SOURCE_DIR}/install/casadi/*)
add_custom_command(TARGET test POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy -t ${CMAKE_SOURCE_DIR}/out ${copy_files}
    )