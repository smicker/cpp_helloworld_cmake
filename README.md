# cpp_helloworld
A basic helloworld program in c++
This also includes some extra stuff that is nice to have like:
- nlohmann/json.hpp for json handling
- utils/date.h for date handling
- utils/Utils.h for some nice helper functions
- Boost (for nice file handling stuff in c++)
- fmt (for modern string handling)
- curl (for getting web pages)
- opencv (for graphics)
- mqtt (for mqtt communication)  

If you don't need one of those, don't install it and remote it from the CMakeLists.txt!!

### Requirements
The following packages needs to be installed (if you want them)
- libfmt-dev (for modern string handling with fmt)
- libcurl14-gnutls-dev (for doing curl calls)
- libboost-all-dev (for Boost)
- libmosquitto-dev libmosquittopp-dev mosquitto-dev (for mqtt)
- OpenCV (see below)

```sudo apt install -y build-essential libboost-all-dev cmake libcurl4-gnutls-dev libfmt-dev libmosquitto-dev libmosquittopp-dev mosquitto-dev```

### How to install OpenCV and libmosquitto for Ubuntu 19.10/18.04

``` bash
$ cd deb_packages
# Open CV 4.5.0
$ sudo apt install ./opencv_1.0.1_amd64.deb
$ sudo apt install ./libmqtt_1.0.0-0_amd64.deb
```

If you want to build OpenCV the old way [see](/docs/opencv.md)

## Installation and compilation
### Create build directory:
``` bash
$ mkdir build
```

### Include paths for OpenCV
You need to run the following in your terminal before building. Alternatively you can enter
the lines at the end of your .bashrc file (that will be executed every time you open your terminal)  
``` bash
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/lib/
```

### Compile this with:
``` bash
$ cd build
$ cmake .. -DCMAKE_PREFIX_PATH=/opt/lib/cmake/opencv4/
$ cd ..
$ make helloworld -C build/
```
Note: this can no longer be built from terminal by g++ in an easy way. And tasks.json is not updated so it cannot be built from VsCode Run -> 'Run without debugging' or Terminal -> 'Run Build Task'. You need to use cmake and make as described above.

### Execute this with:
./build/helloworld

