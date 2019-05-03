# Mongoose CMake wrapper.

This is a simple wrapper allowing to use mongoose library in cmake projects.

### Cloning
To clone this repository use:

`git clone --recurse-submodules https://github.com/memuproject/MongooseCMake.git`

If you want to add this project to your git repository as a submodule use:

`git submodule add https://github.com/memuproject/MongooseCMake.git`

and

`git submodule update --init --recursive`


### Usage
The usage is very simple just link 'mongoose' target to your project.

Example: 
```cmake
add_executable(MyProject
    Main.cpp
)

add_subdirectory("MongooseCMake") # or any other folder where this project is downloaded to
target_link_libraries(MyProject
    PUBLIC
        mongoose
)

```

This will statically link mongoose to your project and make the mogoose.h include available for your source files.