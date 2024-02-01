## Lab-quakes Forecasting

Lab-quakes are simulated earthquake in the lab via an apparatus. You predict an earthquake by predicting when the pressure will be released, which can be achieved by autoregressively modelling the pressure trend and forecast the future pressure.

LLM can be used, since the problem can be modelled with sequences. The only thing that differs is that in earthquakes you have a continuous signal instead of discrete tokens, but the continuous signal can be quantized. The tokens are vectors that represent the shear stress.

Self-supervision is better than supervised learning, since predicting the whole sequence after is a more complex information to learn that a single information (a label). When learning a label, the model can learn a shortcut that may not generalize (feet on the ground → walking). If I force the model to predict the whole sequence, it cannot learn any shortcut, and so I will be sure that it will actually learn.

## Transformers Networks for Trajectory Forecasting

Let’s first formulate the problem: Trajectory forecasting stands for observing $T_{obs}$ Cartesian coordinates (one for each person), and predicting the next future $T_{pred}$ coordinates.

We can consider as inputs either the positions or the speed. Note that we consider the relative position ($x_t - x_0, y_t- y_0)$ and the relative speeds $($$x_t - x_{t-1}, y_t- y_{t-1}$), since the forecasting doesn't depend on the position or the speed of the person in the world.

Usually speed is the preferred representation for most of the cases, since differently from positions, the possible input and output values of speed occupy less space on the cartesian plan, since they are all centered in the zero. This is crucial for the learning since the training data should include all possible coordinates (position or speed), and having less coverage for all the possible input-outputs means that you need less data. If the training data doesn’t cover a part of the plan, then the model won't be able to predict the next step.

Positions are still required when we want to encode the goal coordinates after $t$ timesteps.

We can solve this problem via regression, meaning we predict a set of coordinates and we compute a L2 distance w.r.t. the ground truth in order to have a loss. 

Another approach is to not regress the coordinates, but the mean $\mu_t$ and covariance matrix $\Sigma_t$ for the next $x$ and $y$, in order to model the probability distribution $P(x_t,y_t | x_{t-1}, y_{t-1})$. Then you force the model to shift the mean where the ground truth is, using a negative log-likelihood loss.

In order to make the model transferrable to many different scenes, in addition to the set of coordinates it’s a good idea to also give a context to it, for example by processing the image with a CNN. With this context, the model can know where the subjects of the scene are (a road intersection, a park ecc.) and so it can better know which are the possible trajectories.
