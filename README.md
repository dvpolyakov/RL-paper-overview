# RL-paper-overview
Review of paper https://arxiv.org/pdf/1707.02286.pdf for RL course at YSDA

The best description of resuls is presented on the video: https://www.youtube.com/watch?v=hx_bgoTF7bs

## Task description
- Locomotion task (several bodies with different number of DoFs and actuators
- Input: terrain, set of joints, feet and movement types
- Output: series of motions that maximize reward
- Reward - mainly forward progress. The further we get - the higher the score.
- Challenges: continuous state and action spaces, one sholds design reward carefully
- Additional requirements: robustness and scalability

## Key idea: careful environment design with increasing difficulty level
Training process happens on a rich carefully selected set of challenging levels. The authors found out that rich and robust behaviour will emerge from simple reward functions, if the environment itself contains sufficient richness and diversity
environments include a wide range of obstacles with varying levels of difficulty (e.g. steepness, unevenness, distance between gaps)

The agent faces easier obstacles first and harder obstacles only when it has mastered the easy ones. Also the authors found out that terrains with a “curriculum” of difficulty encourage much more rapid progress than the reward design agents trained in more diverse conditions can be more robust.

<img src="https://i.ibb.co/C1hvP6d/Screenshot-from-2019-03-31-21-46-11.png"> 
The first neural network handles egocentric (sensoric) information (blue). The second network processes environment and task related “exteroceptive” information such as the terrain shape (green)  


## Two modifications of usual learning approaches:
### First: regularization via trust region and proximal optimization
Policy gradient estimates can have high variance - a trust region constraint makes policy gradient algorithms more robust.
Authors used robust policy gradient algorithms, such as trust region policy optimization (TRPO) and proximal policy optimization (PPO), which bound parameter updates to a trust region to ensure stability, making the learning process more robust and less dependent on what parameters we choose. A constraint on how much the policy is allowed to change, expressed in terms of the Kullback-Leibler divergence.

### Second: distributed computations.
Authors distribute the computation over many parallel instances of agent and environment, making the algorithm more scalable - which means that it’s able to efficiently deal with larger problems.

### The algorithm pseudo-code

<img src="https://i.ibb.co/m0W7x0q/Screenshot-from-2019-04-01-16-48-14.png">


## Why is this approach cool?
- no precomputed motion database
- no handcrafting of rewards
- no additional wizardry
- everything is learned from scratch
