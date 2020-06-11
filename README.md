# PID Control Project

## Introduction

The purpose of this project was to build a PID controller and tune the PID hyperparameters by applying the general processing flow as described in the lessons and to test the solution on the simulator.  The simulator provides cross-track error (CTE), speed, and steering angle data via local websocket. The PID (proportional/integral/differential) controller must respond with steering and throttle commands to drive the car reliably around the simulator track.

The project was created with the Udacity [Starter Code](https://github.com/udacity/CarND-PID-Control-Project).

---
## Content of this repo
- `scr` is the directory with the project code.
```
root
|   
|___src
    |   json.hpp
    |   main.cpp
    |   PID.cpp
    |   PID.h
```
  - `main.cpp` -  This file contains the code that will that contains calls to the definition of the PID controller and the PID parameters along with the associated methods.
  - `PID.cpp` - contains the PID methods.
  - `PID.h`- A helpful resource that contains the PID class definition.

---
## Rubric Discussion Points

### Compilation
The code compiles without errors or warnings. No modifications were done on the provided setup.

### Implementation
The PID procedure follows what was taught in the lessons. The PID hyperparameters were tuned and optomized manually by trial and error.

### Reflection
* Effect  of the P, I, D components.*

The P, or "proportional", component had the most directly observable effect on the car's behavior. It caused the car to steer in proportional to the car's distance from the lane center (which is the CTE). Always steering the car towards the lane center while reducing the CTE.

The D, or "differential", component counteracts the P component's tendency to overshoot the center line. A properly tuned D parameter will cause the car to approach the center line smoothly without ringing.

The I, or "integral", component counteracts a bias in the CTE which prevents the P-D controller from reaching the center line. This bias can take several forms, such as a steering drift (as in the Control unit lessons), in this implementation it was observed that the I component appeared to reduce the CTE around curves.

* Chosing the final hyperparameters.*

The Hyperparameters were tuned manually. The narrow track left little room for error, and when attempting to automate parameter optimization it was very common for the car to leave the track. First, it was checked that the car could drive straight with zero as parameters. Next the proportional component was added and the car started following the road but would overshoot. The differential compnent was added to overcome the overshooting. A small component for the integral was added to reduce the steering drift.

The final parameters for P, I, D came out to be 0.15, 0.00001, and 2.5 respectively.

A PID controller for the throttle was also implemented, to reduce the speed if the CTE increased  the car's speed around the track. The throttle PID controller takes the magnitude of the CTE because it wouldn't make sense to change throttle based on the left/right CTE. 

### Simulation
The vehicle could successfully complete a lap around the track without leaving the drivable portion of the track surface.  Here is a link to a short video.

---
## References
The code in this project was adapted from the PID Control course, which was part of Udacity's Self-Driving Car Nanodegree program.