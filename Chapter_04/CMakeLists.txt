cmake_minimum_required(VERSION 3.10)  # Adjust the version based on your CMake version

project(MyGalleryApp)  # You can name your project according to your preference

# Include the subdirectories
add_subdirectory(gallery-core)
add_subdirectory(gallery-desktop)

# Add dependencies
add_dependencies(gallery-desktop gallery-core)
