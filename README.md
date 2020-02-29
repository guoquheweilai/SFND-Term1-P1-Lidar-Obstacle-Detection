# SFND-Term1-P1-Lidar-Obstacle-Detection
Project 1 of Udacity Sensor Fusion Nanodegree
![Overview](/videos/Term1-Project1-Lidar-Obstacle-Detection.gif)  

## (TODO)Overview  
### Welcome to the Sensor Fusion course for self-driving cars.

In this course we will be talking about sensor fusion, whch is the process of taking data from multiple sensors and combining it to give us a better understanding of the world around us. we will mostly be focusing on two sensors, lidar, and radar. By the end we will be fusing the data from these two sensors to track multiple cars on the road, estimating their positions and speed.

**Lidar** sensing gives us high resolution data by sending out thousands of laser signals. These lasers bounce off objects, returning to the sensor where we can then determine how far away objects are by timing how long it takes for the signal to return. Also we can tell a little bit about the object that was hit by measuring the intesity of the returned signal. Each laser ray is in the infrared spectrum, and is sent out at many different angles, usually in a 360 degree range. While lidar sensors gives us very high accurate models for the world around us in 3D, they are currently very expensive, upwards of $60,000 for a standard unit.

**Radar** data is typically very sparse and in a limited range, however it can directly tell us how fast an object is moving in a certain direction. This ability makes radars a very pratical sensor for doing things like cruise control where its important to know how fast the car infront of you is traveling. Radar sensors are also very affordable and common now of days in newer cars.

**Sensor Fusion** by combing lidar's high resoultion imaging with radar's ability to measure velocity of objects we can get a better understanding of the sorrounding environment than we could using one of the sensors alone.  

## Prerequisites/Dependencies  
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)  

## Setup Instructions (abbreviated)  

Meet the [`Prerequisites/Dependencies`](/README.md#L16)  

### Ubuntu 

```bash
$> sudo apt install libpcl-dev
$> cd ~
$> git clone https://github.com/udacity/SFND_Lidar_Obstacle_Detection.git
$> cd SFND_Lidar_Obstacle_Detection
$> mkdir build && cd build
$> cmake ..
$> make
$> ./environment
```

### Windows 

http://www.pointclouds.org/downloads/windows.html

### MAC

#### Install via Homebrew
1. install [homebrew](https://brew.sh/)
2. update homebrew 
	```bash
	$> brew update
	```
3. add  homebrew science [tap](https://docs.brew.sh/Taps) 
	```bash
	$> brew tap brewsci/science
	```
4. view pcl install options
	```bash
	$> brew options pcl
	```
5. install PCL 
	```bash
	$> brew install pcl
	```

#### Prebuilt Binaries via Universal Installer
http://www.pointclouds.org/downloads/macosx.html  
NOTE: very old version 

#### Build from Source

[PCL Source Github](https://github.com/PointCloudLibrary/pcl)

[PCL Mac Compilation Docs](http://www.pointclouds.org/documentation/tutorials/compiling_pcl_macosx.php)  

## Project Description  
Directory Structure
```
.SFND_Lidar_Obstacle_Detection                          # Lidar Obstacle Detection Project
├── CMakeLists.txt                                      # compiler instructions
├── media                                               # media files
│   └── ObstacleDetectionFPS.gif
├── README.md                                           # Readme file
└── src
    ├── environment.cpp                                 # Render car's surrouding environment for visualization
    ├── processPointClouds.cpp                          # Process Lidar data for visualization, source file
    ├── processPointClouds.h                            # Process Lidar data for visualization, header file
    ├── quiz                                            # Quizzes
    │   ├── cluster
    │   │   ├── cluster.cpp                             # Cluster the given point clouds into groups  
    │   │   ├── CMakeLists.txt
    │   │   └── kdtree.h                                # KD tree function for sorting the given point clouds  
    │   └── ransac
    │       ├── CMakeLists.txt
    │       └── ransac2d.cpp                            # Compute random sample consensus on point clouds on a 2D plane  
    ├── render                                          # Render functions
    │   ├── box.h                                       # Draw 3D box around the point clouds  
    │   ├── render.cpp                                  # Render point clouds and other objects
    │   └── render.h                                    # Define libraries and functions for render.cpp
    └── sensors                                         # Recorded Lidar data
        ├── data
        │   └── pcd
        │       ├── data_1
        │       │   ├── 0000000000.pcd
        │       │   ├── 0000000001.pcd
        │       │   ├── 0000000002.pcd
        │       │   ├── 0000000003.pcd
        │       │   ├── 0000000004.pcd
        │       │   ├── 0000000005.pcd
        │       │   ├── 0000000006.pcd
        │       │   ├── 0000000007.pcd
        │       │   ├── 0000000008.pcd
        │       │   ├── 0000000009.pcd
        │       │   ├── 0000000010.pcd
        │       │   ├── 0000000011.pcd
        │       │   ├── 0000000012.pcd
        │       │   ├── 0000000013.pcd
        │       │   ├── 0000000014.pcd
        │       │   ├── 0000000015.pcd
        │       │   ├── 0000000016.pcd
        │       │   ├── 0000000017.pcd
        │       │   ├── 0000000018.pcd
        │       │   ├── 0000000019.pcd
        │       │   ├── 0000000020.pcd
        │       │   └── 0000000021.pcd
        │       ├── data_2
        │       │   ├── 0000000000.pcd
        │       │   ├── 0000000001.pcd
        │       │   ├── 0000000002.pcd
        │       │   ├── 0000000003.pcd
        │       │   ├── 0000000004.pcd
        │       │   ├── 0000000005.pcd
        │       │   ├── 0000000006.pcd
        │       │   ├── 0000000007.pcd
        │       │   ├── 0000000008.pcd
        │       │   ├── 0000000009.pcd
        │       │   ├── 0000000010.pcd
        │       │   ├── 0000000011.pcd
        │       │   ├── 0000000012.pcd
        │       │   ├── 0000000013.pcd
        │       │   ├── 0000000014.pcd
        │       │   ├── 0000000015.pcd
        │       │   ├── 0000000016.pcd
        │       │   ├── 0000000017.pcd
        │       │   ├── 0000000018.pcd
        │       │   ├── 0000000019.pcd
        │       │   ├── 0000000020.pcd
        │       │   ├── 0000000021.pcd
        │       │   ├── 0000000022.pcd
        │       │   ├── 0000000023.pcd
        │       │   ├── 0000000024.pcd
        │       │   ├── 0000000025.pcd
        │       │   ├── 0000000026.pcd
        │       │   ├── 0000000027.pcd
        │       │   ├── 0000000028.pcd
        │       │   ├── 0000000029.pcd
        │       │   ├── 0000000030.pcd
        │       │   ├── 0000000031.pcd
        │       │   ├── 0000000032.pcd
        │       │   ├── 0000000033.pcd
        │       │   ├── 0000000034.pcd
        │       │   ├── 0000000035.pcd
        │       │   ├── 0000000036.pcd
        │       │   ├── 0000000037.pcd
        │       │   ├── 0000000038.pcd
        │       │   ├── 0000000039.pcd
        │       │   ├── 0000000040.pcd
        │       │   ├── 0000000041.pcd
        │       │   ├── 0000000042.pcd
        │       │   ├── 0000000043.pcd
        │       │   ├── 0000000044.pcd
        │       │   ├── 0000000045.pcd
        │       │   ├── 0000000046.pcd
        │       │   ├── 0000000047.pcd
        │       │   ├── 0000000048.pcd
        │       │   ├── 0000000049.pcd
        │       │   ├── 0000000050.pcd
        │       │   ├── 0000000051.pcd
        │       │   ├── 0000000052.pcd
        │       │   ├── 0000000053.pcd
        │       │   ├── 0000000054.pcd
        │       │   ├── 0000000055.pcd
        │       │   ├── 0000000056.pcd
        │       │   ├── 0000000057.pcd
        │       │   ├── 0000000058.pcd
        │       │   ├── 0000000059.pcd
        │       │   ├── 0000000060.pcd
        │       │   ├── 0000000061.pcd
        │       │   ├── 0000000062.pcd
        │       │   ├── 0000000063.pcd
        │       │   ├── 0000000064.pcd
        │       │   ├── 0000000065.pcd
        │       │   ├── 0000000066.pcd
        │       │   ├── 0000000067.pcd
        │       │   ├── 0000000068.pcd
        │       │   ├── 0000000069.pcd
        │       │   ├── 0000000070.pcd
        │       │   ├── 0000000071.pcd
        │       │   ├── 0000000072.pcd
        │       │   ├── 0000000073.pcd
        │       │   ├── 0000000074.pcd
        │       │   ├── 0000000075.pcd
        │       │   ├── 0000000076.pcd
        │       │   ├── 0000000077.pcd
        │       │   ├── 0000000078.pcd
        │       │   ├── 0000000079.pcd
        │       │   ├── 0000000080.pcd
        │       │   ├── 0000000081.pcd
        │       │   ├── 0000000082.pcd
        │       │   ├── 0000000083.pcd
        │       │   ├── 0000000084.pcd
        │       │   ├── 0000000085.pcd
        │       │   ├── 0000000086.pcd
        │       │   ├── 0000000087.pcd
        │       │   ├── 0000000088.pcd
        │       │   ├── 0000000089.pcd
        │       │   ├── 0000000090.pcd
        │       │   ├── 0000000091.pcd
        │       │   ├── 0000000092.pcd
        │       │   ├── 0000000093.pcd
        │       │   ├── 0000000094.pcd
        │       │   ├── 0000000095.pcd
        │       │   ├── 0000000096.pcd
        │       │   ├── 0000000097.pcd
        │       │   ├── 0000000098.pcd
        │       │   ├── 0000000099.pcd
        │       │   ├── 0000000100.pcd
        │       │   ├── 0000000101.pcd
        │       │   ├── 0000000102.pcd
        │       │   ├── 0000000103.pcd
        │       │   ├── 0000000104.pcd
        │       │   ├── 0000000105.pcd
        │       │   ├── 0000000106.pcd
        │       │   ├── 0000000107.pcd
        │       │   ├── 0000000108.pcd
        │       │   ├── 0000000109.pcd
        │       │   ├── 0000000110.pcd
        │       │   ├── 0000000111.pcd
        │       │   ├── 0000000112.pcd
        │       │   ├── 0000000113.pcd
        │       │   ├── 0000000114.pcd
        │       │   ├── 0000000115.pcd
        │       │   ├── 0000000116.pcd
        │       │   ├── 0000000117.pcd
        │       │   ├── 0000000118.pcd
        │       │   ├── 0000000119.pcd
        │       │   ├── 0000000120.pcd
        │       │   ├── 0000000121.pcd
        │       │   ├── 0000000122.pcd
        │       │   ├── 0000000123.pcd
        │       │   ├── 0000000124.pcd
        │       │   ├── 0000000125.pcd
        │       │   ├── 0000000126.pcd
        │       │   ├── 0000000127.pcd
        │       │   ├── 0000000128.pcd
        │       │   ├── 0000000129.pcd
        │       │   ├── 0000000130.pcd
        │       │   ├── 0000000131.pcd
        │       │   ├── 0000000132.pcd
        │       │   ├── 0000000133.pcd
        │       │   ├── 0000000134.pcd
        │       │   ├── 0000000135.pcd
        │       │   ├── 0000000136.pcd
        │       │   ├── 0000000137.pcd
        │       │   ├── 0000000138.pcd
        │       │   ├── 0000000139.pcd
        │       │   ├── 0000000140.pcd
        │       │   ├── 0000000141.pcd
        │       │   ├── 0000000142.pcd
        │       │   ├── 0000000143.pcd
        │       │   ├── 0000000144.pcd
        │       │   ├── 0000000145.pcd
        │       │   ├── 0000000146.pcd
        │       │   ├── 0000000147.pcd
        │       │   ├── 0000000148.pcd
        │       │   ├── 0000000149.pcd
        │       │   ├── 0000000150.pcd
        │       │   ├── 0000000151.pcd
        │       │   ├── 0000000152.pcd
        │       │   └── 0000000153.pcd
        │       └── simpleHighway.pcd
        └── lidar.h                                     # Lidar sensor definition, header file
```

- [CMakeLists.txt](/src/CMakeLists.txt): File to link the C++ code to libraries.  
- [environment.cpp](/src/environment.cpp): C++ script, render car's surrouding environment for visualization  
- [processPointClouds.cpp](/src/processPointClouds.cpp): C++ script, process Lidar data for visualization  
- [processPointClouds.h](/src/processPointClouds.h): Header file, define libraries and functions for processPointClouds.cpp  
- [cluster.cpp](/src/quiz/cluster/cluster.cpp): C++ script, practice your skill on clustering the given point clouds into groups  
- [kdtree.h](/src/quiz/cluster/kdtree.h): Header file, define libraries and functions for KD tree  
- [ransac2d.cpp](/src/quiz/ransac/ransac2d.cpp): C++ script, practice your skill to compute random sample consensus on point clouds on a 2D plane  
- [box.h](/src/render/box.h): Header file, define libraries and functions for drawing 3D box in the environment  
- [render.cpp](/src/render/render.cpp): C++ script, define functions that rendering point clouds and other objects  
- [render.h](/src/render/render.h): Header file, define libraries and functions for render.cpp  
- [lidar.h](/src/sensors/lidar.h): Header file, define libraries and functions for given Lidar sensor  

## Run the project  

* Clone this repository  
```
git clone https://github.com/udacity/SFND_Lidar_Obstacle_Detection.git
```
* Navigate to the `SFND_Lidar_Obstacle_Detection` folder  
```
cd SFND_Lidar_Obstacle_Detection
```
* Create and open `build` folder  
```
mkdir build && cd build
```
* Compile your code  
```
cmake .. && make
```
* Run `environment` application  
```
./environment
```

## Tips  
1. It's recommended to update and upgrade your environment before running the code.  
```
sudo apt-get update && sudo apt-get upgrade -y
```

## Code Style  
Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).  

## Project Rubric  
### 1. Compiling and Testing  
#### 1.1 The submission must compile.  
Yes, it does compile.  
### 2. Obstacle Detection  
#### 2.1 Bounding boxes enclose appropriate objects.  
Yes, it does.  
#### 2.2 Objects are consistently detected across frames in the video.  
Yes, it does.  
#### 2.3 Segmentation is implemented in the project.  
Yes, it does.  
#### 2.4 Clustering is implemented in the project.  
Yes, it does.  
### 3. Code Effciency  
#### 3.1 The methods in the code should avoid unnecessary calculations.  
Yes, it does.  
