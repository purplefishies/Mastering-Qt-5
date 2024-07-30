cmake_minimum_required(VERSION 3.1.0)

project(gallery-desktop)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)

# Find the required Qt packages
find_package(Qt6 COMPONENTS Core Gui Widgets REQUIRED)

# Enable automatic handling of MOC, UIC, and RCC
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Define source and header files
set(SOURCES
    main.cpp
    MainWindow.cpp
    AlbumListWidget.cpp
    AlbumWidget.cpp
    PictureDelegate.cpp
    PictureWidget.cpp
    GalleryWidget.cpp
    ThumbnailProxyModel.cpp
)

set(HEADERS
    MainWindow.h
    AlbumListWidget.h
    AlbumWidget.h
    PictureDelegate.h
    PictureWidget.h
    GalleryWidget.h
    ThumbnailProxyModel.h
)

set(FORMS
    MainWindow.ui
    AlbumListWidget.ui
    AlbumWidget.ui
    PictureWidget.ui
    GalleryWidget.ui
)

set(RESOURCES
    res/resource.qrc
)

# Include path and dependencies for the gallery-core library
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../gallery-core)
link_directories(${CMAKE_CURRENT_BINARY_DIR}/../gallery-core)

# Add executable target
add_executable(gallery-desktop ${SOURCES} ${HEADERS} ${FORMS} ${RESOURCES})

# Link libraries with the target
target_link_libraries(gallery-desktop Qt6::Core Qt6::Gui Qt6::Widgets gallery-core)

# Platform-specific library linking
# if(WIN32)
#     if(CMAKE_BUILD_TYPE MATCHES Release)
#         target_link_libraries(gallery-desktop gallery-core)
#     else()
#         target_link_libraries(gallery-desktop gallery-core)
#     endif()
# else()
#     target_link_libraries(gallery-desktop  gallery-core)
# endif()
