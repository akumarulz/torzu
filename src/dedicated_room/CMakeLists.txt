# SPDX-FileCopyrightText: 2017 Citra Emulator Project
# SPDX-License-Identifier: GPL-2.0-or-later

add_executable(yuzu-room
    precompiled_headers.h
    yuzu_room.cpp
    yuzu_room.rc
)

target_link_libraries(yuzu-room PRIVATE common network)

target_link_libraries(yuzu-room PRIVATE mbedtls mbedcrypto)
if (MSVC)
    target_link_libraries(yuzu-room PRIVATE getopt)
endif()
target_link_libraries(yuzu-room PRIVATE ${PLATFORM_LIBRARIES} Threads::Threads)

if(UNIX AND NOT APPLE)
    install(TARGETS yuzu-room)
endif()

if (YUZU_USE_PRECOMPILED_HEADERS)
    target_precompile_headers(yuzu-room PRIVATE precompiled_headers.h)
endif()

create_target_directory_groups(yuzu-room)
