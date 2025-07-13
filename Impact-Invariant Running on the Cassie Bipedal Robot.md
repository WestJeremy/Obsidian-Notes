https://leggedrobots.org/lrws_2022/contributions.html

**Key words**
Legged Locomotion, traditional control

**Summary of key points** 

**Methodology** 
Model based running controller for bipedal robot Cassie
impact invariant projection
Built in compliance in ankle and knees with springs
Lagrange rigid body dynamic modeling
state contains position and velocity

Model
![[Pasted image 20240222095821.png]]

impact robustness
map contact forces to general accelerations using projection of robot state into the null space of Mass and the Jacobian

[[Operational Space Controller (OSC)]]
optimization problem formulated as quadratic program
![[Pasted image 20240222105939.png]]

![[Pasted image 20240222110014.png]]
state machine {Left stance, Left flight, Right stance, Right flight}


**Results** 
limited velocity variation running gaits
simple controller


**Context**

**Significance** 

**Important Figures and/or Tables and why they are important** 
![[Pasted image 20240222101909.png]]
system block diagram

**Comments** 
I spent some time trying to understand the OSC but am having trouble.
