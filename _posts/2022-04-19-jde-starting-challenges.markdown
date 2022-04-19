---
layout: posts
title:  "Getting Started With GSoC"
date:   2022-04-19 10:17:05 +0530
categories: gsoc22
---
Hey, I am Toshan Luktuke from VJTI, Mumbai. This is the first year I'm applying for GSoC. After looking through a wide variety of organisations, I chose JDE Robot. 
I wanted to do something related to robotics for the summer and JDE perfectly captured my interests of robotics and engaging teaching.

## Getting Started
I started by heading over to the offical website of JDE, there they had an entire page dedicated to GSOC. I looked through the projects and selected the two that seemed the most interesting to me:
- [Improvement of Visual Circuit](https://jderobot.github.io/activities/gsoc/2022#project-7-improvement-of-visualcircuit-web-service)
- [Deep Learning for Visual Control](https://jderobot.github.io/activities/gsoc/2022#project-5-robotics-academy-new-exercise-using-deep-learning-for-visual-control)

## Challenges!
The next step was to contact the mentors, but wait! We had to complete some challenges first.
These served as asort of litmus test to show your interest and dedication to the project.

There were two compulsory and two optional challenges, I decided to do all of them. :smile:

### Programming Challenges
There were two challeneges for [C++]() and [Python]().
The C++ challenge was quite interesting.
It involved tracing the longest path possible through a labyrinth composed of **#**'s with **.**'s as the path.
My initial thought was to use some sort of reverse heuristic approach to get the longest path. However, I quickly abandonded that idea as we had to always find the longest path and heuristic apporaches are not guaranteed to find this path everytime. 

I settled on a recursive backtracking approach and it worked like a charm. Another challenge was using `CMAKE's` build system, it took a bit of trial and error to get everything working propoerly.

For the Python Challenge, we had to simulate the movement of a particle. I did this using `matplotlib` and its animate class.
Since I had prior experience with how particles work due to previous projects, this one was quite simple.

### Robotics Academy
The next challenge involved solving one exercise from JDE's Robot Academy. Here we had to install the Docker container that contains these exercises. I followed their official instructions for the same. 
I faced some issues with enabling hardware acceleration. However despite trying many different alternatives, I couldn't use my Nvidia GPU with the Docker Image at the end.

I decided to take up the PID Racecar Exercise as the simulation was working pretty well despite not using my graphics card.  
After playing around with JDE's `HAL` and `GUI` classes, some revision of Colour Filters in CV2 and a lot of PID tuning later:
<iframe width="560" height="315" src="https://www.youtube.com/embed/wbu0eO-DN-k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### ROS2 Challenge

I installed ROS2 Foxy from the [official site](https://docs.ros.org/en/foxy/Installation/Ubuntu-Development-Setup.html).

Following which I followed their [tutorial](https://docs.ros.org/en/foxy/Tutorials/Writing-A-Simple-Py-Publisher-And-Subscriber.html) for setting up a simple publisher and subscriber.

The last task here was to run a robot and visualize its laser scan data using `rviz`. To do this I chose the `dummy_robot` that is included with your ROS2 install. 
I [followed](https://docs.ros.org/en/foxy/Tutorials/dummy-robot-demo.html) this tutorial for getting the dummy_robot up and running. After that it was a simple matter of adding a LaserScan element to `Rviz` and viola:

<img src="https://github.com/toshan-luktuke/JDE_Challenges/blob/main/assets/Laser_Scan.gif">

### Turtlebot Challenge
I followed [this](https://automaticaddison.com/how-to-install-ros-2-navigation-nav2/) guide for the install of the turtlebot pre-requisites.
It worked pretty well except for a memorable error.

In the current ROS2 install, the sourcing is done via the downloaded repo
```bash
. ~/ros2_foxy/install/local_setup.bash
```
However while following the install guide I had installed some packages in the local directory, so I had to do
```bash
source /opt/ros/foxy/setup.bash
```

Since I hadn't done this before there were a few errors with `CMAKE_SOURCE_PATH` while installing the required `nav2` packages. However after the above command was run, it worked like a charm.

I did some reverse engineering using the `RQT` tool in ROS2 to figure out which topic Position messages were being sent to. My search led me to the `/goal_pose` topic. From then it was a simple matter of writing a Python script to publish `PoseStamped()` messages to the topic, and watch the bot move via script.

<iframe width="560" height="315" src="https://www.youtube.com/embed/GzRo4oeLvBo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Repository link: [https://github.com/toshan-luktuke/JDE_Challenges](https://github.com/toshan-luktuke/JDE_Challenges)
