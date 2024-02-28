---
Exam:
  - Advanced Machine Learning
---
SimSiam is a modification of the [[BYOL]] architecture, where they replace the momentum projector and the momentum encoder with the same projector and encoder from the left branch, but add a stop gradient technique (you don’t back propagate on the right branch).

![Screenshot 2024-01-13 at 3.16.16 PM.png](Screenshot_2024-01-13_at_3.16.16_PM.jpeg)

SimSiam has better performances for the first epochs of training, while is outperformed by BYOL in the long run (over 200 epochs).

![Screenshot 2024-01-13 at 3.19.45 PM.png](Screenshot_2024-01-13_at_3.19.45_PM.jpeg)

![Screenshot 2024-01-13 at 3.20.00 PM.png](Screenshot_2024-01-13_at_3.20.00_PM.jpeg)
