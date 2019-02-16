
### [Udacity Self-Driving Car Nanodegree: Programming a Real Self-Driving Car](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2/modules/e1a23b06-329a-4684-a717-ad476f0d8dff/lessons/462c933d-9f24-42d3-8bdc-a08a5fc866e4/concepts/5ab4b122-83e6-436d-850f-9f4d26627fd9) 

## [Final Capstone Project](https://github.com/fwa785/CarND-Capstone.git)


## Team Knight Riders' KITT


##### * Feng Wang -- fwa785@gmail.com
##### * Maria Cristina An -- jingle1216@yahoo.com
##### * Carlos Barredo -- ccbaes@yahoo.es
##### * Stavros Dimopoulos -- sdim@sdim.gr
##### * Venkata Ramesh Gudapati -- venkataramesh@gmail.com


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
The team members have the option to choose which environment to install and work their project on: Docker, AWS, VM and the Udacity Workspace were the preferred containers. Data was also shared via the FTP server. Work was done in phases as described as discussed below.


#### Classifier


The team used [__Google's Tensorflow Object Detection API__](https://github.com/tensorflow/models/blob/master/research/object_detection) for its code framework and have tested on multiple models before arriving at their final choice: the [**Single Shot MultiBox Detector with the Inception Neural Network v2 trained on the Coco dataset 2018 01 28**](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md).


#### Training


Training was done on two separate annotated datasets taken online. The first dataset contains simulator images that was fed to the model to create the first inference graph for running the classifier in the simulator. The training took *2,970 steps*. The second dataset contains real-life images mixed with Carla ROS bag images for running on Carla and it took *3,900 steps*. One team member's PC acted as a server to hold the huge data files necessary for training the models which cannot be loaded in Github since it imposes a 50MB file size limitation. 


### Project Construction


#### Timeline


To complete the tasks on time, the KITT team has followed a schedule as well as the [order of project development](https://classroom.udacity.com/nanodegrees/nd013/parts/6047fe34-d93c-4f50-8336-b70ef10cb4b2 "System Integration Project Lesson 4. Project Overview") suggested in the classroom.


#### Bottlenecks


* The first issue faced by the team was on which model to use for the project. *Speed* versus *accuracy* were the usual factors considered. Nevertheless, *latency* became a major determinant since the car would not run because of it. The models that were tried on were the Faster RCNN, SSD Resnet and SSD Inception. The latter became the best choice for its low computational overhead.

* Acquisition of good annotated data was done online, both for the sim images and the site images.

* A major hurdle for everyone was in setting up the environment for the project. A significant proportion of the time was spent on getting the project to run in the one environment, only to change to another because of high latency or non-workable errors. Some team members actually had to downgrade the systems they were using to meet the code requirements for Carla.
  and  

* Building the classifier was the last difficulty for the team. Trial and error were done every step of the way. The buildup phases were as follows:
	* classifying red light, no red light using sim images
	* classifying with the state/colors
	* overcoming the car's sluggish motion with the color addition 
	* classifying with real-life images
	* overcoming latency
	* downgrading to meet Carla requirements

The final draft now runs on Tensorflow-GPU 1.3 with CUDA 8.0 with two inference graphs for running in both the simulator and Carla's system.


### Directions For Use


* Follow instructions to build the workstation, install ROS and the _unity_ simulator from the [Udacity repository](https://github.com/udacity/CarND-Capstone.git)
* Download code from [this repository](https://github.com/fwa785/CarND-Capstone.git).
* Download inference graphs from the [ftp server](ftps://carnd:addas_engrs_2019@CarND.sdim.gr).
* Run the simulator.

The End
