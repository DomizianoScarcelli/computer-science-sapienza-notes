---
Exam:
  - Advanced Machine Learning
---
We can describe the state of the world with $S$ with a continuous or a discrete representation. $s$ on the other hand is the state we’re interested in.

$a$ is the set of actions that the robot can perform. The policy function $\pi(a | s)$ can be a deep learning model that assigns an action for each possible state.

There also is a transition probability $P(s' | a, s)$ which give us the probability of ending in the state $s'$ by performing action $a$ in the state $s$. This is very difficult to model.

We also know that this transition probability is subject to the Markov property, which means that $s ^{(t+1)}$ is conditionally independent from $s ^{(t-1)}$ if I know $s ^{(t)}$. In other word, the state only conditionally depend on the previous state, and I don't care about all the other past.

The policy is what we train, but we need to define the good and the bad actions. We do that with a reward function, which assigns a score for each action performed in a certain state.

A trajectory $\tau$ is the ordered sequence of state and actions $s_1, a_2,\dots, s_T, a_t$. We can compute the probability $p_\theta(\tau)$ . We use that to compute the objective, which is the set of parameters that maximises the expected value of the reward function under the trajectory distribution.

In order to remove the expected value we just sample a large number of trajectories. With this trick I can approximate the expected value.

There is a problem tough: we need to compute the gradient of something we don’t know (the initial state and the system dynamics). Because of that, we need to remove these values from the expectation.

The REINFORCE algorithm works in this way: you fit a model to estimate the return, you use that to improve the policy, and then you run the policy to generate some samples and do that until convergence.

This algorithm during the years has been modified a lot. 

Point Goal Navigation is the task where a robot is put in a random starting position and orientation in an environment it has never seen, and it’s asked to navigate to the target coordinates. There is no map available, and the robot only has it’s sensors (camera and gps, which is essential to know how distant it’s from the goal coordinates). This task is pretty much solved, with some algorithms with a really high accuracy. The problem is that, if there are other entities in the world, the robot doesn't know how to navigate without hitting them, this is why we need social navigation for.

The task is to spawn a certain number of robots in an area, and each one of them has to perform point goal navigation without hitting each other. The difficulty is for a robot to predict the trajectory of other robots in order to avoid them, and avoid to slow down them.

In order to evaluate a robot social navigation algorithm, researchers have defined some basic principles:

![Screenshot 2024-01-16 at 6.59.09 PM.png](Screenshot_2024-01-16_at_6.59.09_PM.jpeg)

Legibility means that the actions the robots do should be understood by other entities. In the picture the robots announces that it’s going through a sharp edge to tell the person that it's coming on the other side.

The policy is what we train for. We can also inject a risk value in the architecture, in order for the robot to know how risky it is to take a certain path and not collide with another entity.

HM3D-S is a large scale dataset which contains 3D scans of houses. The evaluation metrics are:

![Screenshot 2024-01-16 at 7.17.41 PM.png](Screenshot_2024-01-16_at_7.17.41_PM.jpeg)

SPL: difference between the optimal path and the one taken by the robot.