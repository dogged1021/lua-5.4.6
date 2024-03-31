# 所有的头文件和c文件生成lua54动态库
aux_source_directory ( ${SRC} SOURCE_FILES )
list ( REMOVE_ITEM SOURCE_FILES ${SRC}/luac.c ${SRC}/lua.c )
add_library ( lua54 STATIC ${SOURCE_FILES} )

add_executable ( lua lua.c )
target_link_libraries ( lua lua54 )

add_executable ( luac luac.c )
target_link_libraries ( luac lua54 )

file ( COPY lua.h lauxlib.h lua.hpp luaconf.h lualib.h DESTINATION ${LUA}/include )

if ( WIN32 )
    install ( TARGETS lua luac
        RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
    )
    install ( TARGETS lua54
        ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
    )
    install ( FILES lua.h lauxlib.h lua.hpp luaconf.h lualib.h
        DESTINATION ${CMAKE_INSTALL_PREFIX}/include
    )
endif ( WIN32 )
