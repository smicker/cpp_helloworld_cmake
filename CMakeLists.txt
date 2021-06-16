cmake_minimum_required(VERSION 3.10)
set(CMAKE_CXX_STANDARD 17)
# Set compiler flags, Wall for extra warnings, pedantic for more warnings regarding extensions,
# pthread for being able to do threading in c++.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -pthread")
set(CMAKE_C_COMPILER "gcc-7")
set(CMAKE_CXX_COMPILER "g++-7")
project(helloworld)

# Don't know what below is used for.
#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

# Include package fmt (for formatting text. This needs to be installed separately)
find_package(fmt REQUIRED)

# Include Boost components
find_package(Boost 1.65 COMPONENTS system thread program_options filesystem REQUIRED)
include_directories(${Boost_INCLUDE_DIR})

# Include curl
find_package(CURL REQUIRED)
include_directories(${CURL_INCLUDE_DIR})

# Include OpenCV
set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} /opt/lib)
include_directories(/opt/include)
find_package(OpenCV REQUIRED)

# Include MQTT
find_package(PkgConfig REQUIRED)
set(MQTT_LIB
    /opt/lib/libmosquitto.so
    /opt/lib/libmosquittopp.so
)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

file(GLOB helloworld_SRC
     "*.h"
     "*.cpp"
     "utils/*.cpp"
     "nlohmann/*.cpp"
)
list(REMOVE_ITEM Multipart_SRC "${CMAKE_SOURCE_DIR}/awsDemo.cpp") # Remove awsDemo.cpp since we don't want to build that

add_executable(helloworld ${helloworld_SRC}) #Add app's main starting file.

target_link_libraries(helloworld ${Boost_LIBRARIES} ${MQTT_LIB} ${CURL_LIBRARIES} ${OpenCV_LIBS} fmt::fmt stdc++fs)