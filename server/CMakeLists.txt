cmake_minimum_required(VERSION 3.13)
cmake_policy(VERSION 3.13)

etn_target(exe ${PROJECT_NAME}
    SOURCES
        src/*.cpp
        src/*.h

    USES_PRIVATE
        cxxtools
        fty_common
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
