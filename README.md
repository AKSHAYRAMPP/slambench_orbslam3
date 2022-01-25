# SLAMBench - ORB_SLAM3
Paper

Robust SLAM Systems: Are We There Yet?

[https://robustslam.github.io/evaluation](https://robustslam.github.io/evaluation)

Original repo : [https://github.com/pamela-project/slambench](https://github.com/pamela-project/slambench)

## What is SLAMBench?

SLAMBench is a SLAM performance benchmark that combines a framework for quantifying quality-of-result with instrumentation of accuracy, execution time, memory usage and energy consumption. It also include a graphical interface to visualize these information.

SLAMBench offers a platform for a broad spectrum of future research in jointly exploring the design space of algorithmic and implementation-level optimisations. It targets desktop, laptop, mobile and embedded platforms. Some of the benchmarks (in particular KFusion) were tested on Ubuntu, OS X and Android (more information about android here [https://github.com/bbodin/slambench-android](https://github.com/bbodin/slambench-android)).

SLAMBench currently supports the following algorithms:

   ORB-SLAM3 [Campos et al, ARXIV'20]: C++ as distributed by [https://github.com/UZ-SLAMLab](https://github.com/UZ-SLAMLab)
   
   ReFusion [Palazollo et al. IROS'19]: CUDA as distributed by [https://github.com/PRBonn](https://github.com/PRBonn)
    
   OpenVINS [Geneva et al. IROS'19]: C++ as distributed by [https://github.com/rpng/](https://github.com/rpng/)
    
   Supereight [Vespa et al. RA-L'18]: C++, OpenMP as distributed by [https://github.com/rpng/](https://github.com/emanuelev)
    
   BundleFusion [Dai et al. ACM TOG'17]: CUDA as distributed by [https://github.com/niessner](https://github.com/niessner)
    
   SemanticFusion [McCormac et al. ICRA'17]: CUDA as distributed by [https://github.com/seaun163](https://github.com/seaun163)
    
   ORB-SLAM2 [Mur-Artal et al, TOR'15 and TOR'17]: C++ as distributed by [https://github.com/raulmur](https://github.com/raulmur)
    
   DSO [Engel et al. Arxiv'16]: C++ as distributed by [https://github.com/JakobEngel](https://github.com/JakobEngel)
    
   ElasticFusion [Whelan et al, IJRR'16]: CUDA as distributed by [https://github.com/mp3guy](https://github.com/mp3guy)
    
   InfiniTAMv2 [Kahler et al, ISMAR'15]: C++, OpenMP and CUDA versions as distributed by [https://github.com/victorprad/](https://github.com/victorprad/)
    
   KinectFusion [Newcombe et al. ISMAR'11]: C++, OpenMP, OpenCL and CUDA inspired by [https://github.com/GerhardR](https://github.com/GerhardR)
    
   LSDSLAM [Engel et al, ECCV'14]: C++, and threaded as distributed by [https://github.com/tum-vision/](https://github.com/tum-vision/) and modified by [https://github.com/mp3guy](https://github.com/mp3guy)
    
   MonoSLAM [Davison et al, TPAMI'07]: Original version as distributed by [https://github.com/hanmekim/](https://github.com/hanmekim/)
    
   OKVIS [Leutenegger et al, IJRR'15]: Original version as distributed by [https://github.com/ethz-asl](https://github.com/ethz-asl)
    
   PTAM [Klein et al, ISMAR'07 and ECCV'08]: Original version as distributed by [https://github.com/Oxford-PTAM/](https://github.com/Oxford-PTAM/)
    
   SVO [Forster et al, ICRA'14]: Original version as distributed by [https://github.com/uzh-rpg/rpg_svo/](https://github.com/uzh-rpg/rpg_svo/) (a more recent version available at [http://rpg.ifi.uzh.ch/svo2.html](http://rpg.ifi.uzh.ch/svo2.html))

IMPORTANT: If you use any of those algorithms in scientific publications, you should refer to the respective publications.


## How to set up SLAMBench?

As SLAMBench deals with multiple SLAM algorithms, dependencies might be difficult to install on any systems. To ease the usage of SLAMBench we provide auto-installation of dependencies and recommend the use fresh installation of Ubuntu 18/20 or Fedora 24-29.
Dependency installation
Required by SLAMBench framework

    CMake 2.8.11 or higher is required.
    Make
    GCC C/C++
    Boost (Optional)
    GLUT (Optional)

Required by benchmarks and datasets

    Git
    Mercurial
    wget
    unzip
    lapack
    blas
    findutils
    cvs
    glog
    gflags
    p7zip

To install them

With Ubuntu 20.04: `apt-get -y install libvtk6.3 libvtk6-dev unzip libflann-dev wget mercurial git gcc g++ cmake python-numpy freeglut3 freeglut3-dev libglew-dev libglu1-mesa libglu1-mesa-dev libgl1-mesa-glx libgl1-mesa-dev libxmu-dev libxi-dev libboost-all-dev cvs libgoogle-glog-dev libatlas-base-dev gfortran gtk2.0 libgtk2.0-dev libyaml-dev build-essential libyaml-cpp-dev`

## Special requirements for CUDA

To run the CUDA implementation of some of the algorithms, you will need extra dependencies.

With Ubuntu: `apt-get -y install nvidia-cuda-toolkit clinfo`

## Setting up slambench

Alog: ORB_SLAM3
Dataset: EuRoC MAV [Burri et al, IJRR'16]: Micro Aerial Vehicle dataset (machine_hall/MH_01_easy)

`git clone https://github.com/pamela-project/slambench`

`cd slambench`

`make deps`

`make slambench`

Edit **benchmarks.makefile** inside **/slambench/framework/makefiles** and add 

```jsx
@echo -n "  - ORBSLAM3 [Campos et al, ARXIV'20] : " ; if [ -d benchmarks/orbslam3/src/original ] ; then echo -e "\033[1;32mFound\033[0m" ; else echo -e "\033[1;31mNot found (make orbslam3)\033[0m" ; fi
@echo    "    repository: https://github.com/UZ-SLAMLab"
@echo    "    available targets are : orbslam3"
@echo    ""
```

and

```jsx
orbslam3:
@echo "================================================================================================================="
@echo    "  - ORBSLAM3 [Campos et al, ARXIV'20] "
@echo    "    Original repository: https://github.com/UZ-SLAMLab"
@echo    "    Used repository: https://github.com/mihaibujanca/ORB_SLAM3"
@echo "================================================================================================================="
@echo ""
@echo "Are you sure you want to download this use-case (y/n) ?" && ${GET_REPLY} && echo REPLY=$$REPLY && if [ ! "$$REPLY" == "y" ] ; then echo -e "\nExit."; false; else echo -e "\nDownload starts."; fi
mkdir -p benchmarks/orbslam3/src/original
rm benchmarks/orbslam3/src/original -rf
git clone https://github.com/mihaibujanca/ORB_SLAM3 benchmarks/orbslam3/src/original
@echo "cmake_minimum_required(VERSION 2.8)"   > benchmarks/$@/CMakeLists.txt
@echo "explore_implementations ( $@ src/* )"     >> benchmarks/$@/CMakeLists.txt
```

in appropriate area.

`make orbslam3`

`cd slambench/benchmarks/orbslam3/src/original/Thirdparty/DBoW2`

`mkdir build && cd build`

`cmake .. -DCMAKE_BUILD_TYPE=Release`

`make -j2`

`cd slambench/benchmarks/orbslam3/src/original/Thirdparty/g2o`

`mkdir build && cd build`

`cmake .. -DCMAKE_BUILD_TYPE=Release`

`make -j2`

`cd slambench/benchmarks/orbslam3/src/original/Vocabulary`

`tar -xf ORBvoc.txt.tar.gz`

`cd slambench`

`make slambench APPS=orbslam3`

using EuRoC MAV [Burri et al, IJRR'16]: Micro Aerial Vehicle dataset

`make datasets/EuRoCMAV/machine_hall/MH_01_easy/MH_01_easy.slam`

# Runing benchmark

`./build/bin/slambench -i datasets/EuRoCMAV/machine_hall/MH_01_easy/MH_01_easy.slam -load ./build/lib/libORB_SLAM3-original-library.so -m mono`

# Errors

In case of segmentation fault, remove **-march=native** from these flags

`set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -march=native")`

`set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -march=native")`

inside the CMakeLists.txt file in */slambench/benchmarks/orbslam3/src/original/Thirdparty/DBoW2* **,** */slambench/benchmarks/orbslam3/src/original/Thirdparty/g2o* and */slambench/benchmarks/orbslam3/src/original*

After making changes in the files remove build folder from the above folders and rebuild it.

