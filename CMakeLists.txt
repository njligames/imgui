cmake_minimum_required(VERSION 3.5.1)

# add the binary tree directory to the search path 
# for include files
include_directories( ${CMAKE_CURRENT_SOURCE_DIR} )
 
SET(imgui_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp
    )

SET(imgui_HDRS
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui.h
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui_internal.h
    ${CMAKE_CURRENT_SOURCE_DIR}/imconfig.h 
    ${CMAKE_CURRENT_SOURCE_DIR}/stb_rect_pack.h
    ${CMAKE_CURRENT_SOURCE_DIR}/stb_textedit.h
    ${CMAKE_CURRENT_SOURCE_DIR}/stb_truetype.h
    )

# add the main library
if(BUILD_STATIC_LIB)
  ADD_LIBRARY(imgui STATIC ${imgui_SRCS} ${imgui_HDRS})
endif()

if(BUILD_SHARED_LIB)
  ADD_LIBRARY(imgui SHARED ${imgui_SRCS} ${imgui_HDRS})
endif()
 
install (TARGETS imgui DESTINATION ${CMAKE_INSTALL_LIBDIR})
install (FILES imgui.h imgui_internal.h imconfig.h stb_textedit.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

foreach(p LIB INCLUDE)
    set(var CMAKE_INSTALL_${p}DIR)
    if(NOT IS_ABSOLUTE "${${var}}")
        set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    endif()
endforeach()
