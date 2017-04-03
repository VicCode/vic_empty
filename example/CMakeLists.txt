#Find all source files in a directory.
aux_source_directory(./ ${PROJECT_NAME}_example_src_list)

if (BUILD_STATIC_LIBRARY)
    message(STATUS "STATIC ${PROJECT_NAME}")
    set(${PROJECT_NAME}_example_link_lib
    #    liba_a
        ${PROJECT_NAME}_a
    )
    set(${PROJECT_NAME}_example_dependencies
        ${PROJECT_NAME}_a
    #    liba_a
    )
else()
    message(STATUS "SHARED ${PROJECT_NAME}")
    set(${PROJECT_NAME}_example_link_lib
    #    liba_so
        ${PROJECT_NAME}_so
    )
    set(${PROJECT_NAME}_example_dependencies
        ${PROJECT_NAME}_so
    #    liba_so
    )
endif()

#if(LIBUNWIND)
#    list(APPEND ${PROJECT_NAME}_example_link_lib ${LIBUNWIND})
#endif()
#if(LIBLZMA)
#    list(APPEND ${PROJECT_NAME}_example_link_lib ${LIBLZMA})
#endif()
#if(LIBRT)
#    list(APPEND ${PROJECT_NAME}_example_link_lib ${LIBRT})
#endif()

if(${PROJECT_NAME}_example_src_list)
    message(STATUS "【${PROJECT_NAME}_example】: ${${PROJECT_NAME}_example_src_list}")

    foreach(${PROJECT_NAME}_example_src ${${PROJECT_NAME}_example_src_list})
        get_filename_component(${PROJECT_NAME}_example_bin ${${PROJECT_NAME}_example_src} NAME_WE)
        add_executable(${${PROJECT_NAME}_example_bin} ${${PROJECT_NAME}_example_src})
        if(${PROJECT_NAME}_example_link_lib)
            target_link_libraries(${${PROJECT_NAME}_example_bin} ${${PROJECT_NAME}_example_link_lib})
        endif()
        if(${PROJECT_NAME}_example_dependencies)
            add_dependencies(${${PROJECT_NAME}_example_bin} ${${PROJECT_NAME}_example_dependencies})
        endif()
    endforeach()
else()
    message(STATUS "【${PROJECT_NAME}_example】 not has src")
endif()

