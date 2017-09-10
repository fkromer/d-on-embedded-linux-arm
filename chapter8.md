# Introduction

In the following sections you will get some quick start guideance about how to get started with D development on embedded Linux
running on ARM processors.The BeagleBone Black is used as exemplary embedded Linux development board. A lot of documentation with
relation to common topics like the boards system architecture, hardware, etc. is available in the internet and in books.

## The intent

Helping others to learn how to use D in an embedded Linux environment.

## The vision

My personal vision is to use D in robotics.

This projects shall help people to get started doing something like this
[chair climbing humanoid robot controlled by a BeagleBone (Youtube)](https://www.youtube.com/watch?v=jRlIESXSh1Y)
which is [programmed in C++](https://github.com/jcbrenes/Bioloid-Locomotion-API)
or this [self-balancing robot controlled by a BeagleBone (Youtube)](https://www.youtube.com/watch?v=gDG2rSBdcVo)
with an implementation in D instead.

By providing a port of the existing [main ROS client libraries](http://wiki.ros.org/Client%20Libraries)
(C++, Python, Lisp) as experimental ROS client library implemeneted in D (like
e.g. Java, Go, etc.) ROS nodes implemented in D could be used as part of a ROS
based system. This would ease the creation of robots like the one above using the
ROS framework.

[Educational Robotics Critical for the Future of Linux (YouTube)](https://www.youtube.com/watch?v=DNu33mV13LI#t=28m34s)
