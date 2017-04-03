#Find all source files in a directory.
set(LIB_NAME_EMPTY "${PROJECT_NAME}")
message(STATUS "LIB_NAME: ${LIB_NAME_EMPTY}")

aux_source_directory(./ ${LIB_NAME_EMPTY}_src_list)

if(${LIB_NAME_EMPTY}_src_list)
    message(STATUS "【${LIB_NAME_EMPTY}】: ${${LIB_NAME_EMPTY}_src_list}")

    #Static library
    if(BUILD_STATIC_LIBRARY)
        message(STATUS "STATIC ${LIB_NAME_EMPTY}")
        add_library(${LIB_NAME_EMPTY}_a STATIC ${${LIB_NAME_EMPTY}_src_list})
        set_target_properties(${LIB_NAME_EMPTY}_a PROPERTIES OUTPUT_NAME "${LIB_NAME_EMPTY}")
        install(TARGETS ${LIB_NAME_EMPTY}_a DESTINATION lib)
    endif()

    #Shared library
    if(BUILD_SHARED_LIBRARY)
        message(STATUS "SHARED ${LIB_NAME_EMPTY}")
        add_library(${LIB_NAME_EMPTY}_so SHARED ${${LIB_NAME_EMPTY}_src_list})
        set_target_properties(${LIB_NAME_EMPTY}_so PROPERTIES OUTPUT_NAME "${LIB_NAME_EMPTY}")
        set_target_properties(${LIB_NAME_EMPTY}_so PROPERTIES VERSION ${${LIB_NAME_EMPTY}_VERSION} SOVERSION ${${LIB_NAME_EMPTY}_VERSION_MAJOR})
        install(TARGETS ${LIB_NAME_EMPTY}_so DESTINATION lib)
    endif()
else()
    message(STATUS "【${LIB_NAME_EMPTY}】 not has src")
endif()

