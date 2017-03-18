#Find all source files in a directory.
aux_source_directory(./ ${PROJECT_NAME}_src_list)

if(${PROJECT_NAME}_src_list)
    message(STATUS "【${PROJECT_NAME}】: ${${PROJECT_NAME}_src_list}")
else()
    message(STATUS "【${PROJECT_NAME}】 not has src")
    return()
endif()

#Static library
if(BUILD_STATIC_LIBRARY)
    message(STATUS "STATIC ${PROJECT_NAME}")
    add_library(${PROJECT_NAME}_a STATIC ${${PROJECT_NAME}_src_list})
    set_target_properties(${PROJECT_NAME}_a PROPERTIES OUTPUT_NAME "${PROJECT_NAME}")
    install(TARGETS ${PROJECT_NAME}_a DESTINATION lib)
endif()

#Shared library
if(BUILD_SHARED_LIBRARY)
    message(STATUS "SHARED ${PROJECT_NAME}")
    add_library(${PROJECT_NAME}_so SHARED ${${PROJECT_NAME}_src_list})
    set_target_properties(${PROJECT_NAME}_so PROPERTIES OUTPUT_NAME "${PROJECT_NAME}")
    set_target_properties(${PROJECT_NAME}_so PROPERTIES VERSION ${${PROJECT_NAME}_VERSION} SOVERSION ${${PROJECT_NAME}_VERSION_MAJOR})
    install(TARGETS ${PROJECT_NAME}_so DESTINATION lib)
endif()

