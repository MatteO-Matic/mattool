cmake_minimum_required(VERSION 3.5)

project(MatMemTool)
SET(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB SOURCES "*.c")

# Define an executable
add_executable(matmem ${SOURCES})

target_compile_options(matmem PRIVATE -Wall -fsanitize=address -fsanitize=leak -g
    -DKMOD_MEMMAP -D_DEFAULT_SOURCE
    -D_POSIX_C_SOURCE=200809L -pedantic -DMVERBOSE=4 -DMTR_ENABLED -DREAD_CHECK
    -Wno-padded -Wno-sign-conversion -Wno-missing-variable-declarations
    -Wno-weak-vtables -Wno-missing-prototypes)

# Define the libraries this project depends upon
target_link_libraries(matmem asan dl pthread)
# target_link_options

#set(THREADS_PREFER_PTHREAD_FLAG ON)
#find_package(Threads REQUIRED)
#target_link_libraries(server Threads::Threads)
