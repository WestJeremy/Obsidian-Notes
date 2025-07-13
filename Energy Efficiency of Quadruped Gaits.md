Silva, M. F., and J. A. Tenreiro Machado. “Energy Efficiency of Quadruped Gaits.” _CLAWAR_, Springer Berlin Heidelberg, 2006, pp. 735–42, https://doi.org/10.1007/3-540-26415-9_88.

**Key words**
gaits
efficiency


**Summary of key points** 
Gaits may be described in words walk, trot, run, gallop, bound.
Body height should decrease as velocity increases 
Stride length should increase as velocity increases

**Methodology** 
Models for Energy usage and hip deviation are created
${E_{av}}=\frac{1}{d} {\Sigma} { \Sigma}\int_{a}^{b} {\tau(t)}^{2} \dot{\theta}(t) \,dt$
A variety of gaits are defined with control parameters
Energy efficiency and hip deviation are evaluated at a range of velocities at specific gaits.

**Results** 
Given a set of robot parameters, ideal gaits for target velocities were defined.
Body height should decrease as velocity increases.
Stride length should increase as velocity increases.

**Context**
The work proposes models for energy consumption and path deviation
The work asserts that body height and stride length relate to efficiency.
These parameters are trivial and may be useful terms in the Neural Net.


(how this article relates to other work in the field; how it ties in with key issues and findings by others) 

**Significance** 
Establishes body height and stride length as possible parameters for the NN


**Important Figures and/or Tables and why they are important** 
![[Pasted image 20240110165504.png]]
Top: Energy vs velocity of 3 gaits
Energy usage peaks around different velocities.
Forcing a walking gait to move quickly (which many companies do) is shown to increase energy consumption linearly while other methods dramatically decrease energy usage.

Bottom Left: Velocity vs Stride Length
Roughly linear

Bottom Right: Body Height vs Velocity
Roughly linear



![[Pasted image 20240110165537.png]]

Left: Energy vs velocity for 3 different gaits
Right: Hip deviation from path vs velocity for 4 different gaits


**Comments** 
Note the plots do not use consistent gaits.
It seems like there might be some cherry picking data going on here to show the cleanest results.
Might also just be showing off different gaits.

