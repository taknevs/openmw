project(luasocket_ext C)

# 1. Search for Lua 5.1 headers specifically
find_path(LUA_CUSTOM_INCLUDE_DIR NAMES lua.h
    PATHS 
    /usr/include/lua5.1
    /usr/include/luajit-2.1
    /usr/include/lua5.4
    /usr/include
)

if(NOT TARGET luasocket)
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
        auxiliar.c
        compat.c
        usocket.c
    )

    add_library(luasocket STATIC ${LUASOCKET_SRC})

    # 2. Force the compiler to use the path we found
    target_include_directories(luasocket PRIVATE ${LUA_CUSTOM_INCLUDE_DIR})
    
    # 3. Also include the folder luasocket.h is in
    target_include_directories(luasocket PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

    # 4. Link against the library
    target_link_libraries(luasocket PRIVATE ${LUA_LIBRARIES})

    if(NOT WIN32)
        target_compile_definitions(luasocket PRIVATE LUASOCKET_API=)
    endif()
endif()

# Debug message so you can see if it worked during 'cmake ..'
message(STATUS "LUASOCKET: Using Lua headers from: ${LUA_CUSTOM_INCLUDE_DIR}")
