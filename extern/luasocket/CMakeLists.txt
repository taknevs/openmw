project(luasocket)

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
    usocket.c # This is the Unix-specific file for Linux
)

add_library(luasocket STATIC ${LUASOCKET_SRC})

# Ensure the compiler can find the headers in this directory
target_include_directories(luasocket PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})