cmake_minimum_required (VERSION 3.1)

project (PROJECT_NAME)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Enable C++ 17
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_SUPPRESS_REGENERATION true)

# set qt library path - Here set the Qt Library Path, below is an example
set(CMAKE_PREFIX_PATH  "C:/Qt/Qt5.12.6/5.12.6/msvc2017")

# Now set qt libs path - Here I have just added some examples of most used libs to get started
set(Qt5_DIR  ${CMAKE_PREFIX_PATH}/lib/cmake/lib/cmake/Qt5)
set(Qt5Core_DIR  ${CMAKE_PREFIX_PATH}/lib/cmake/Qt5Core)
set(Qt5Gui_DIR  ${CMAKE_PREFIX_PATH}/lib/cmake/Qt5Gui)
set(Qt5Widgets_DIR  ${CMAKE_PREFIX_PATH}/lib/cmake/Qt5Widgets)
set(Qt5Sql_DIR  ${CMAKE_PREFIX_PATH}/lib/cmake/Qt5Sql)
set(Qt5Network_DIR ${CMAKE_PREFIX_PATH}/lib/cmake/lib/cmake/Qt5Network)

# Instruct Cmake to run CMAKE_AUTOMOC, CMAKE_AUTOUIC, CMAKE_AUTORCC
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# Find the Qt library
find_package(Qt5Core CONFIG REQUIRED)
find_package(Qt5Widgets CONFIG REQUIRED)
find_package(Qt5Gui CONFIG REQUIRED)
find_package(Qt5Sql CONFIG REQUIRED)
find_package(Qt5Network CONFIG REQUIRED)

# Globs all the files and adds to the exe
file(GLOB_RECURSE SOURCE_FILES "*.cc" "*.h" "*.ui" "*.qrc" "*.rc")
foreach(_source IN ITEMS ${SOURCE_FILES})
    get_filename_component(_source_path "${_source}" PATH)
    string(REPLACE "${CMAKE_SOURCE_DIR}" "" _group_path "${_source_path}")
    string(REPLACE "/" "\\" _group_path "${_group_path}")
    source_group("${_group_path}" FILES "${_source}")
endforeach()
	
add_executable(	PROJECT_NAME 
				WIN32 
				${SOURCE_FILES})

target_link_libraries(PROJECT_NAME Qt5::Core)
target_link_libraries(PROJECT_NAME Qt5::Widgets)
target_link_libraries(PROJECT_NAME Qt5::Gui)
target_link_libraries(PROJECT_NAME Qt5::Sql)
target_link_libraries(PROJECT_NAME Qt5::Network)