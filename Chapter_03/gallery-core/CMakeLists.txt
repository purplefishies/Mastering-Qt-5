cmake_minimum_required(VERSION 3.1.0)

project(gallery-core)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)

# Define a macro
add_definitions(-DGALLERYCORE_LIBRARY)

# Find the required Qt packages
find_package(Qt6Sql REQUIRED)

# Exclude the GUI module
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Define source and header files
set(SOURCES
    AlbumModel.cpp
    DatabaseManager.cpp
    Album.cpp
    Picture.cpp
    PictureModel.cpp
    AlbumDao.cpp
    PictureDao.cpp
)

set(HEADERS
    gallery-core_global.h
    AlbumModel.h
    DatabaseManager.h
    Album.h
    Picture.h
    PictureModel.h
    AlbumDao.h
    PictureDao.h
)

# Add a library target
add_library(gallery-core ${SOURCES} ${HEADERS})

# Link Qt6Sql
target_link_libraries(gallery-core Qt6::Sql)
