Markov Decision Process
State space based decision maker, partly on data, partly random


![[Pasted image 20240205114631.png]]
S Set of states(state Space)
A set of all Action spaces (As Action available to a given state S)
Pa(s,s')=Pr(st+1=s' |  st=s, at=a)   probability action a in state s at time t will lead to state s' at time t+1
Ra(s,s') the immediate reward received after transitioning from state s to s' due to action a


Optimization objective
find a function PI that specifies the action pi(s) that the decision maker will choose when in state s. 

ML Reinforcement learning
