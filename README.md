### [Udacity Self-Driving Car Nanodegree](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2/modules/e1a23b06-329a-4684-a717-ad476f0d8dff/lessons/462c933d-9f24-42d3-8bdc-a08a5fc866e4/concepts/5ab4b122-83e6-436d-850f-9f4d26627fd9) 


# [Final Capstone Project: Programming a Real Self-Driving Car](https://github.com/fwa785/CarND-Capstone.git)


#### presented by:
### Team Knight Riders' KITT


#### * Feng Wang -- fwa785@gmail.com
#### * Maria Cristina An -- jingle1216@yahoo.com
#### * Carlos Barredo -- ccbaes@yahoo.es
#### * Stavros Dimopoulos -- sdim@sdim.gr
#### * Venkata Ramesh Gudapati -- venkataramesh@gmail.com


--------------


### Project Overview


This final project is submitted in fulfillment of the requirements for the Self-Driving Car Engineer Nanodegree Program. It is summarized into the following phases: 

1. Building the Team
2. Project Description
3. Project Construction
4. Directions for Use


### Building the Team


The team members are part of the November 2018 cohort, most of which have an engineering or robotics background. 
The tasks for the project were divided by nodes except for the classifier where everyone took part in acquiring and annotating data, testing models and consolidating a run successfully. Communication was through a group Slack channel and the team created its own  repository under it's team leader's account. The KITT Github repository can be found [here](https://github.com/fwa785/CarND-Capstone.git).


### Project Description


#### Model


The goal of the project is to write a code that will drive the car around a road track in a simulation after which the same code will be applied to drive a real car **Carla** around a real-life track. 
The project's code was structured using ROS packages wrapped in a Catkin workspace, written in Python and C++.
The team members have the option to choose which environment to install and work their project on: Docker, AWS, VM and the Udacity Workspace were the preferred containers. Data was also shared via the FTP server. Work was done in phases as described below.


#### Classifier


The team used [__Google's Tensorflow Object Detection API__](https://github.com/tensorflow/models/blob/master/research/object_detection) for its classifier framework and have tested on multiple models before arriving at their final choice: the [**Single Shot MultiBox Detector with the Inception Neural Network v2 trained on the Coco dataset 2018 01 28**](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).


#### Training


Training was done on two separate annotated datasets taken online. The first dataset contains simulator images that was fed to the model to create the first inference graph for running the classifier in the simulator. The training took *2,970 steps*. The second dataset contains real-life images mixed with Carla ROS bag images for running on Carla and it took *3,900 steps*. One team member's PC acted as a server to hold the huge data files necessary for training the models which cannot be loaded in Github since it imposes a 50MB file size limitation. 


### Project Construction


#### Timeline


To complete the tasks on time, the KITT team has followed a schedule as well as the [order of project development](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2 "System Integration Project Lesson 4. Project Overview") suggested in the classroom.


#### Bottlenecks


* The first issue faced by the team was on which model to use for the project. *Speed* versus *accuracy* were the usual factors considered. Nevertheless, *latency* became a major determinant since the car would not run because of it. The models that were tried on were the Faster RCNN, SSD Resnet and SSD Inception. The latter became the best choice for its low computational overhead.

* Acquisition of good annotated data was done online, both for the sim images and the site images.

* A major hurdle for everyone was in setting up the environment for the project. A significant proportion of the time was spent on getting the project to run in the one environment, only to change to another because of high latency or non-workable errors. Some team members actually had to downgrade the systems they were using to meet the code requirements for Carla.


* Building the classifier was the last difficulty for the team. Trial and error were done every step of the way. The buildup phases were as follows:
	* classifying red light, no red light using sim images
	* classifying according to state/colors
	* overcoming the car's sluggish motion with the addition of color classifier
	* classifying with real-life images
	* overcoming latency
	* downgrading to meet Carla requirements

The final draft now runs on Tensorflow-GPU 1.3 with CUDA 8.0 with two inference graphs for running in both the simulator and Carla's system.


### Directions For Use

Please use **one** of the two installation options, either native **or** docker installation.

### Native Installation

* Be sure that your workstation is running Ubuntu 16.04 Xenial Xerus or Ubuntu 14.04 Trusty Tahir. [Ubuntu downloads can be found here](https://www.ubuntu.com/download/desktop).
* If using a Virtual Machine to install Ubuntu, use the following configuration as minimum:
  * 2 CPU
  * 2 GB system memory
  * 25 GB of free hard drive space

  The Udacity provided virtual machine has ROS and Dataspeed DBW already installed, so you can skip the next two steps if you are using this.

* Follow these instructions to install ROS
  * [ROS Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu) if you have Ubuntu 16.04.
  * [ROS Indigo](http://wiki.ros.org/indigo/Installation/Ubuntu) if you have Ubuntu 14.04.
* [Dataspeed DBW](https://bitbucket.org/DataspeedInc/dbw_mkz_ros)
  * Use this option to install the SDK on a workstation that already has ROS installed: [One Line SDK Install (binary)](https://bitbucket.org/DataspeedInc/dbw_mkz_ros/src/81e63fcc335d7b64139d7482017d6a97b405e250/ROS_SETUP.md?fileviewer=file-view-default)
* Download the [Udacity Simulator](https://github.com/udacity/CarND-Capstone/releases).

### Docker Installation
[Install Docker](https://docs.docker.com/engine/installation/)

Build the docker container
```bash
docker build . -t capstone
```

Run the docker file
```bash
docker run -p 4567:4567 -v $PWD:/capstone -v /tmp/log:/root/.ros/ --rm -it capstone
```

### Port Forwarding
To set up port forwarding, please refer to the [instructions from term 2](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/16cf4a78-4fc7-49e1-8621-3450ca938b77)

### Usage

1. Clone the project repository
```bash
git clone https://github.com/fwa785/CarND-Capstone.git
```

2. Copy the frozen graph files
Get the frozen graph files from gdrive location https://drive.google.com/open?id=1FERKyNAq_J4phr7LbAKs_s4EH5-K7GTU,
and copy the files to ros/src/tl_detector directory

3. Install python dependencies
```bash
cd CarND-Capstone
pip install -r requirements.txt
```
4. Make and run styx
```bash
cd ros
catkin_make
source devel/setup.sh
roslaunch launch/styx.launch
```
5. Run the simulator

### Real world testing
1. Download [training bag](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/traffic_light_bag_file.zip) that was recorded on the Udacity self-driving car.
2. Unzip the file
```bash
unzip traffic_light_bag_file.zip
```
3. Play the bag file
```bash
rosbag play -l traffic_light_bag_file/traffic_light_training.bag
```
4. Launch your project in site mode
```bash
cd CarND-Capstone/ros
roslaunch launch/site.launch
```
5. Confirm that traffic light detection works on real life images
