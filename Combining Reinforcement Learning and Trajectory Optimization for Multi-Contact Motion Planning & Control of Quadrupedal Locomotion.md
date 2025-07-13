https://leggedrobots.org/lrws_2022/contributions.html

**Key words**

Legged Robots; Deep Learning in Robotics and Automation; Motion and Path planning; Reinforcement Learning; Quadrupedal Robots;


**Summary of key points** 
model-based Trajectory Optimization and model-free DRL methods to enable quadrupedal systems to traverse complex non-flat terrain"

"Trajectory Optimization (TO) technique for determining so-called transition feasibility between discrete support phases using a coarse model of the robot....removes the need for a planner to interact with both physics and a motion controller during training, allows the two policies to be trained independently"

"Gait Planner with Nonlinear Model Predictive Controller (NMPC)"

transition feasibility criterion realized as a TO problem

**Methodology** 

Markov Decision Process [[MDP]]

Gait planner gets data of surrounding ground
GP Generates gait params and base motions towards a certain heading


"GP is realized as stochastic policy parameterized using Neural Network (NN) function approximation, and policy search is performed using state-of-the-art DRL algorithms"

![[Pasted image 20240202113436.png]]

"the inclusion of the angular momentum in the decision variables whilst also directly parameterizing the centroid’s linear and angular trajectories using a uniform time discretization instead of employing Bezier curves."

-Momentum is going to impact feasibility and efficiency.


**Results** 
foothold and gait planning for terrain-ware quadrupedal locomotion on rigid non-flat terrain with floor map

Solving for both gait and footholds simultaneously using Deep Reinforcement Learning (DRL)

"... the need for a planner to interact with both physics and a motion controller during training...allows the two policies to be trained independently."

Training of physics and motion controller is separated

**Context**


(how this article relates to other work in the field; how it ties in with key issues and findings by others) 

**Significance** 


**Important Figures and/or Tables and why they are important** 
![[Pasted image 20240202120645.png]]


**Comments** 
Gaits are going to be efficiency vs stability and the feasibility coefficient could help


