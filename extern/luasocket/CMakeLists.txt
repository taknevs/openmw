project(luasocket C)

set(LUASOCKET_SRC
    luasocket.c
    timeout.c
    buffer.c
    io.c
    select.c
    options.c
    inet.c
    tcp.c
    udp.c
    except.c
    auxiliar.c   # Added: Handles class/group management
    compat.c     # Added: Provides luasocket_setfuncs for different Lua versions
    usocket.c    # Unix-specific file for Linux/Mint
)

add_library(luasocket STATIC ${LUASOCKET_SRC})

# Ensure the compiler can find the headers in this directory
target_include_directories(luasocket PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Professional touch: define LUASOCKET_API as empty for static linking on Linux
if(NOT WIN32)
    target_compile_definitions(luasocket PRIVATE LUASOCKET_API=)
endif()
