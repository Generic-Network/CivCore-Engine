cmake_minimum_required(VERSION 3.31)


set(CMAKE_TOOLCHAIN_FILE "${CMAKE_CURRENT_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake"
        CACHE STRING "Vcpkg toolchain file")

project(engine)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)



find_package(fmt CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)

add_executable(engine
        src/main.cpp
        src/io/util/parseConfig.cpp
        src/io/util/parseConfig.h
        src/header/config.h
        src/datapull/pullDataUsr.cpp
        src/datapull/pullDataUsr.h
        src/datapull/pullDataSpdr.cpp
        src/datapull/pullDataSpdr.h
        src/com/estbComFD.cpp
        src/com/estbComFD.h
        src/com/httpReqResHandler.cpp
        src/com/httpReqResHandler.h
        src/io/util/logsys/logsys.cpp
        src/io/util/logsys/logsys.h
)

file(COPY src/config.json DESTINATION ${CMAKE_BINARY_DIR})


target_include_directories(engine PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src/header
        ${CMAKE_CURRENT_SOURCE_DIR}/Libraries/include
)


target_link_libraries(engine
        PRIVATE
        fmt::fmt
        spdlog::spdlog

)


if(WIN32)
    target_link_libraries(engine PRIVATE ws2_32 mswsock)
endif()
