cmake_minimum_required(VERSION 3.13)
cmake_policy(VERSION 3.13)

project(fty-alert-srr
    VERSION 1.0.0
    DESCRIPTION "SRR agent for alert configuration"
)

##############################################################################################################
find_package(fty-cmake PATHS ${CMAKE_BINARY_DIR}/fty-cmake)
##############################################################################################################

add_subdirectory(server)
