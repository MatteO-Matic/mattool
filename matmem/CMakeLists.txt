cmake_minimum_required(VERSION 3.5)
#project(libjsonutils VERSION 1.0.0 LANGUAGES CXX)
project(MatMemTool)
SET(CMAKE_EXPORT_COMPILE_COMMANDS ON)


file(GLOB SOURCES "*.c")

#set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fsanitize=address -fsanitize=leak -g")
#target_compile_features(app PRIVATE cxx_std_17)

#compile_args_external = ['-DLMODE=MODE_EXTERNAL', '-fsanitize=address']

#dl = meson.get_compiler('c').find_library('dl', required : false)
#thread = meson.get_compiler('c').find_library('pthread', required : false)

#base_files = ['mem.c', 'wintools.c', 'pmparser.c']
#hlapi_files = ['hlapi/windll.cpp', 'hlapi/winprocess.cpp', 'hlapi/winprocesslist.cpp']

# link_args_external = ['-lasan']

#try_args = ['-Weverything', '-Wno-padded', '-Wno-sign-conversion', '-Wno-padded', '-Wno-documentation-unknown-command', '-Wno-missing-variable-declarations', '-Wno-c++98-compat', '-Wno-c++98-compat-pedantic', '-Wno-weak-vtables', '-Wno-old-style-cast']
#try_args_c = ['-Wno-missing-prototypes']

# Define an executable
add_executable(matmem ${SOURCES})

#compile_args = ['-D_POSIX_C_SOURCE=200809L', '-pedantic', '-DMVERBOSE=4', '-DMTR_ENABLED', '-DREAD_CHECK']

# KDIR := /lib/modules/$(shell uname -r)/build
target_compile_options(matmem PRIVATE -Wall -fsanitize=address -fsanitize=leak -g
    -DKMOD_MEMMAP
    -D_POSIX_C_SOURCE=200809L -pedantic -DMVERBOSE=4 -DMTR_ENABLED -DREAD_CHECK
    -Wno-padded -Wno-sign-conversion -Wno-missing-variable-declarations
    -Wno-weak-vtables -Wno-missing-prototypes)

# Define the libraries this project depends upon
target_link_libraries(matmem asan dl pthread)
# target_link_options

#set(THREADS_PREFER_PTHREAD_FLAG ON)
#find_package(Threads REQUIRED)
#target_link_libraries(server Threads::Threads)
