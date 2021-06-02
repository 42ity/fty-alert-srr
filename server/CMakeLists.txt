cmake_minimum_required(VERSION 3.13)
cmake_policy(VERSION 3.13)

project(fty-alert-srr
    VERSION 1.0.0
    DESCRIPTION "SRR agent for alert configuration"
)

##############################################################################################################
find_package(fty-cmake PATHS ${CMAKE_BINARY_DIR}/fty-cmake)
##############################################################################################################

# set(CMAKE_BUILD_TYPE Debug)

etn_target(exe ${PROJECT_NAME}
    SOURCES
        src/alert/rule.cpp
        src/alert/rule.h
        src/alert/rule_manager.cpp
        src/alert/rule_manager.h
        src/config/config.cpp
        src/config/config.h
        src/srr/alert-srr.cpp
        src/srr/alert-srr.h
        src/utils/messages.cpp
        src/utils/messages.h
        src/utils/serialization.cpp
        src/utils/serialization.h
        src/fty-alert-srr.cpp
    USES_PRIVATE
        cxxtools
        fty_common_dto
        fty_common_logging
        fty_common_messagebus
        protobuf
        pthread
        stdc++fs
)

##############################################################################################################

install(FILES conf/fty-alert-srr.cfg DESTINATION ${CMAKE_INSTALL_FULL_SYSCONFDIR}/fty-alert-srr/)

# systemd unit
etn_configure_file(
    systemd/${PROJECT_NAME}.service.in
    TARGET      ${PROJECT_NAME}
    DESTINATION "${CMAKE_INSTALL_PREFIX}/lib/systemd/system/"
)

##############################################################################################################
