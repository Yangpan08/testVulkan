set(target_name "01_template")

find_package(Vulkan)

if(NOT Vulkan_FOUND)
    message(FATAL_ERROR "Vulkan not found")
else()
    message(${Vulkan_INCLUDE_DIRS})
    message(${Vulkan_INCLUDE_DIR})
    message(${Vulkan_LIBRARY})
    message(${Vulkan_LIBRARIES})
endif()

add_executable(${target_name} "main.cpp")

target_include_directories(${target_name} PRIVATE ${PROJECT_SOURCE_DIR}/3rdparty/includes)
target_link_directories(${target_name} PRIVATE ${PROJECT_SOURCE_DIR}/3rdparty/libs/$<IF:$<CONFIG:Debug>,Debug,Release>/${CMAKE_HOST_SYSTEM_NAME})

target_include_directories(${target_name} PRIVATE ${Vulkan_INCLUDE_DIR})

target_link_libraries(${target_name} PRIVATE glfw3 ${Vulkan_LIBRARIES})

install(TARGETS ${target_name} RUNTIME DESTINATION )

