# Setup project
cmake_minimum_required(VERSION 3.0)
project(Mongoose)

# Create library
add_library(mongoose SHARED mongoose/mongoose.c)

# Set C Standard
set_property(TARGET mongoose PROPERTY C_STANDARD 11)

# Create includes directory
set(MONGOOSE_INCLUDE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/includes")
file(REMOVE_RECURSE ${MONGOOSE_INCLUDE_DIRECTORY})
file(MAKE_DIRECTORY ${MONGOOSE_INCLUDE_DIRECTORY})
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/mongoose/mongoose.h" DESTINATION ${MONGOOSE_INCLUDE_DIRECTORY})

# Add includes to the target
target_include_directories(mongoose
    PUBLIC
        ${MONGOOSE_INCLUDE_DIRECTORY}
)

# Find Threads
set(CMAKE_THREAD_PREFER_PTHREAD ON)
find_package(Threads)

if (Threads_FOUND)
    target_compile_definitions(mongoose
        PUBLIC
            -DMG_ENABLE_THREADS
    )

    target_link_libraries(mongoose
        PUBLIC
            Threads::Threads
    )
endif()
