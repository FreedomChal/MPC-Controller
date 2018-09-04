# Model Predictive Control
Classwork for the Udacity Self Driving Car Nanodegree

## Model Predictive Controller Description

A Model Predictive Controller (MPC) is a method of trajectory optimization. Upon receiving current trajectory data, the current location, and a polynomial approximation of the best possible trajectory, the MPC plans the optimal trajectory given the current information. After moving in accordance to the optimal trajectory, the system pauses for a small period of time called a "timestep", and the process is run again. Often the method of optimization is tweaked by penalizing sharp turns and accelerations. Also, in this project, there is a small latency between commands. As a result, part of the model designing is finding a solution to prevent latency from being a problem.

## MPC Design

### MPC Process

The purpose of my MPC is to control a car driving in the [term 2 simulator](https://github.com/udacity/self-driving-car-sim).
My MPC design is very similar to the course's "Mind the Line" quiz solution, and uses many pieces of code from said solution. The process followed by my MPC design starts with the extraction of the location and trajectory data. Following this is one of the few parts of the model that are not in the "Mind the Line" quiz. To deal with latency, the x and y coordinates and psi are changed as if the car had driven for the latency duration plus an extra computing time at a constant velocity. I got the idea for this from [here](https://github.com/gardenermike/model-predictive-controller/blob/master/src/main.cpp). After this data tweak, the coordinates of the waypoints (points used to represent the center of the road in the simulator) are converted to vehicle coordinates. Then, I use the provided polyfit function to fit a third degree polynomial to the waypoints. This is then used to calculate the vehicle state. Following this, the actual solving part of the MPC is run. The data is then formatted, sent to the simulator, and the process is restarted.

### Loss Function

The optimization part of MPCs works by minimizing what is called the "loss". This loss is calculated by a "loss function", which when given certain data calculates the loss. The loss function I used is almost identical to the one used in Mind the Line. The cross track error and orientation error each squared are added to the loss. Next, the throttle squared and steering angle squared are also added to the loss. Finally, the difference in throttle and steering between timesteps squared is added to the loss.

### Hyperparameters

#### N

I started with a N (number of points planned ahead) of five. I found that this value worked well for planning ahead far enough, but did not result in excessive computation requirements. I never made many changes to N following the original setting.

#### dt

As with N, I did not make many changes to dt. I chose 0.1 for dt, which worked well computationally, and also was small enough to acknowledge new information.

#### Reference Velocity

The final reference velocity I used was 30 mph. I could have made it larger, and was previously, but I was experiencing problems with lag, which enormously decreases how well the car drives. I was doing my project development in a virtual machine which had limited memory, and experienced extreme lag in the simulator, which was the main problem. To deal with this, I later ran the simulator on my local machine instead, which fixed the lag problem. If you experience lag in the simulator, I would recommend using lower quality graphics in the simulator. Doing this helps a lot.
