# Model Predictive Control
Classwork for the Udacity Self Driving Car Nanodegree

## Model Predictive Controller Description

A Model Predictive Controller (MPC) is a method of trajectory optimization. Upon receiving current trajectory data, the current location, and a polynomial approximation of the best possible trajectory, the MPC plans the optimal trajectory given the current information. After moving in accordance to the optimal trajectory, the system pauses for a small period of time called a "timestep", and the process is run again.
