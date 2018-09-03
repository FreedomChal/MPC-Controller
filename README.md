# Model Predictive Control
Classwork for the Udacity Self Driving Car Nanodegree

## Model Predictive Controller Description

A Model Predictive Controller (MPC) is a method of trajectory optimization. Upon receiving current trajectory data, the current location, and a polynomial approximation of the best possible trajectory, the MPC plans the optimal trajectory given the current information. After moving in accordance to the optimal trajectory, the system pauses for a small period of time called a "timestep", and the process is run again. Often the method of optimization is tweaked by penalizing sharp turns and accelerations. Also, in this project, there is a small latency between commands. As a result, part of the model designing is finding a solution to prevent latency from being a problem.

## MPC Design

My MPC design is very similar to the course's "Mind the Line" quiz solution, and uses many pieces of code from said solution. The process followed by my MPC design starts with the extraction of the location and trajectory data. Following this is one of the few parts of the model that are not in the "Mind the Line" quiz. To deal with latency, the x and y coordinates and psi are changed as if the car had driven for the latency duration plus an extra computing time at a constant velocity. I got the idea for this from [here](https://github.com/gardenermike/model-predictive-controller/blob/master/src/main.cpp). After this data tweak, 
