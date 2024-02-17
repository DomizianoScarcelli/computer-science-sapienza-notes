---
Exam:
  - Deep Learning
---
### Double Descent (Capacity-wise)

[[Early Stopping]] can be done in with respect to two dimensions: capacity of the model and training time.

![Screenshot 2023-04-12 at 5.01.07 PM.png](Screenshot_2023-04-12_at_5.01.07_PM.png)

From this plot we can see how is the trend of training and validation data, varying the capacity $\mathcal{H}$ of the model, meaning each time we increase the number of parameters of the model, train it for a fixed number of epochs, and see what is the final validation error.

In order to perform early stopping, we will choose the model that yields the validation error that is in the *sweet spot*. However, if we carry on for a long time, it can happen that the validation error will go down again, in a phenomenon known as *double descent*.

This makes sense since increasing the capacity of the model to a very large value, the model will be always more expressive, and at one point will express perfectly the true unknown function that describes the data.

The surprising fact is that [[Gradient Descent#Stochastic gradient descent|SGD]] is able to find such good models.

### Double Descent (Epoch-wise)

As said before, early stopping can also happen with respect to training time, meaning that if we train the model long enough, the validation error will go down again.

![Bluer the color, lower the validation error.](Screenshot_2023-04-12_at_5.11.34_PM.png)

The bluer the color, the lower the validation error.