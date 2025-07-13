https://arxiv.org/abs/2209.05309

**Key words**
Legged Locomotion, Reinforcement Learning, Transfer Learning

**Summary of key points** 
Most controllers are robot specific
If we can take into account the model of the robot we can make a network that can control any robot without retraining.

**Methodology** 
Randomize the morphology of the robot
Simulate with a wide variety of randomized robots
More general control strategies will be acquired

Vary size, length mass of robot
scale PD gains with mass

**Results** 
Successfully ran AnyMal and mini cheetah which were never explicitly trained

"we found that our approach was able to produce effective policies with fully feedforward neural networks. By taking in past observations and actions as input, the model is able to to implicitly encode task-relevant information about the robot’s morphology, and successfully transfer locomotion skills across a diverse set of quadrupedal morphologies without requiring an explicit representation of a particular robot’s body structure."

**Context**
"Graph convolutional networks have been used to implicitly encode the morphological structure of simulated robots with varying numbers of degrees-of-freedom "

(how this article relates to other work in the field; how it ties in with key issues and findings by others) 

**Significance** 


**Important Figures and/or Tables and why they are important** 
![[Pasted image 20240215092806.png]]

$\Phi$ includes everything in the robot's current state
$\Phi$ feeds through GenLoco and 
Output added to nominal joint positions
Movements are passed through a low pass filter to stop high frequency movements
Move then sent to PD joint control.

**Comments** 
This is really exciting stuff. A generalized network that doesn't take robot parameters as an input should also be more resistant to inaccuracies in the model because there isn't a model. 



