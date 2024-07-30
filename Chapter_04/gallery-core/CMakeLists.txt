cmake_minimum_required(VERSION 3.10)
project(gallery-core)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find the required Qt packages
find_package(Qt6 COMPONENTS Core Sql REQUIRED)

# Exclude the GUI module
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Add a library target called gallery-core
add_library(gallery-core SHARED
    AlbumModel.cpp
    DatabaseManager.cpp
    Album.cpp
    Picture.cpp
    PictureModel.cpp
    AlbumDao.cpp
    PictureDao.cpp
)

# Include directories for the target
target_include_directories(gallery-core PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Define the preprocessor macros
target_compile_definitions(gallery-core PRIVATE GALLERYCORE_LIBRARY)

# Link the required Qt libraries
target_link_libraries(gallery-core Qt6::Core Qt6::Sql)
