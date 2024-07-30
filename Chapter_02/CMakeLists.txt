cmake_minimum_required(VERSION 3.5)

project(ch02-sysinfo VERSION 1.0.0 LANGUAGES CXX)

# Set C++14 standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find the necessary Qt6 modules
find_package(Qt6 COMPONENTS Core Gui Widgets Charts REQUIRED)

# Define the sources and headers
set(SOURCES
    main.cpp
    MainWindow.cpp
    SysInfo.cpp
    CpuWidget.cpp
    MemoryWidget.cpp
    SysInfoWidget.cpp
)

set(HEADERS
    MainWindow.h
    SysInfo.h
    CpuWidget.h
    MemoryWidget.h
    SysInfoWidget.h
)

# Conditional source files based on platform
if(WIN32)
    list(APPEND SOURCES SysInfoWindowsImpl.cpp)
    list(APPEND HEADERS SysInfoWindowsImpl.h)
elseif(UNIX AND NOT APPLE)
    list(APPEND SOURCES SysInfoLinuxImpl.cpp)
    list(APPEND HEADERS SysInfoLinuxImpl.h)
elseif(APPLE)
    list(APPEND SOURCES SysInfoMacImpl.cpp)
    list(APPEND HEADERS SysInfoMacImpl.h)
endif()

# Include UI file
set(FORMS MainWindow.ui)

# Setup executable
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS} ${FORMS})

# Link against Qt libraries
target_link_libraries(${PROJECT_NAME} Qt6::Core Qt6::Gui Qt6::Widgets Qt6::Charts)

# Enable AUTOUIC for processing forms, AUTOMOC for moc headers, and AUTORCC for resources
set_target_properties(${PROJECT_NAME} PROPERTIES
    AUTOUIC ON
    AUTOMOC ON
    AUTORCC ON
)

