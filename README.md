# slambench_orbslam3

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

