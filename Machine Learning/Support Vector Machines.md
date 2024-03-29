---
Exam:
  - Fundamentals of Data Science
---
Support Vector Machines are another classifier that allows to build a non linear decision boundary much like multinomial logistic regression, but without having to manually choose the variations of the features ($x^2, \sqrt{x}, x^2 \sqrt[3]{x}$ etc.).

The main concepts behind how a SVM work are Optimal Margin Classifiers and Kernels.

## Optimal Margin Classifier

For now we assume that the dataset is separable, meaning it can exists a linear boundary that separates the examples.

### Functional Margin

- Recap on how binary classification works in logistic regression
    
    $$
    h_\theta(x) = g(\theta^Tx)
    $$
    
    The classifier predicts $1$ if $\theta^Tx > 0$, and $0$ otherwise. This because $\theta^Tx > 0 \Rightarrow h_\theta(x) \ge 0.5$.
    
    In other words, this means that if $y^{(i)}=1$, we hope that $\theta^Tx \gg 0$;
    if $y^{(i)} = 0$, we hope that $\theta^Tx \ll 0$. 
    

<aside>
💡 **New notation:**

- Labels $y \in \{-1,+1\}$
- $h$ output values in $\{-1, +1\}$ and not a probability
- $g(z) = 
\begin{cases}
1 && \text{if } z \ge 0 \\
-1 && \text{otherwise}
\end{cases}$
- $h_{w,b}(x) = g(w^Tx+b)$ where $x \in \R^n$ and $b \in \R$. (We drop the $x_0=1$ convention)
</aside>

### Functional margin of hyerplane defined by  $(w,b)$ with respect to $(x^{(i)}, y^{(i)})$

The parameters $w,b$ defines an hyperplane, that in just a higher dimension line that seprarates the samples.

We define the functional margin as following:

$$
\hat{\gamma}^{(i)} = y^{(i)}(w^Tx^{(i)}+b)
$$

As before for logistic regression:

- If $y^{(i)} = 1$, we want and hope that $w^Tx^{(i)}+b \gg 0$;
- If $y^{(i)} = 0$, we want and hope that $w^Tx^{(i)}+b \ll 0$

And this means that we want and hope that $\hat{\gamma}^{(i)} \gg 0$.

We can define the functional margin with respect to the entire training set as:

$$
\hat{\gamma} =\min_{i=1}^n{ \hat{\gamma}^{(i)}}
$$

There is a problem here, since it’s possible to “cheat” and change the functional margin, without influencing the decision boundary, by just multiplying for the same factor both the parameters $w$ and $b$.

In order to solve this problem, is to normalize the length of the parameters. One way of doing this is forcing the magnitude of the vector to be 1 ($\lVert x\rVert=1$), or by replacing $(w,b)$ with $(\frac{w}{\lVert w \rVert}, \frac{b}{\lVert b \rVert})$.

### Geometric Margin

The geometric margin describes how much the decision boundary stands apart from the examples. A decision boundary that separates best the points, meaning that doesn't comes very close to some training samples, has a larger geometric margin hence is better.

More formally, the geometric margin is the euclidean distance between the training sample coordinates and the line (or hyperplane) that represents the decision boundary.

We formally define the geometric margin with respect to a particular training sample $(x^{(i)}, y^{(i)})$ as:

$$
\gamma^{(i)} = \frac{y^{(i)}(w^Tx^{(i)}+b)}{\lVert x \rVert}
$$

We can define the geometric margin with respect to entire training set as the worst gemetric margin w.r.t a particular training sample:

$$
\gamma =\min_{i=1}^n{ \gamma^{(i)}}
$$

We can now see that the geometric margin and the functional margin are correlated:

$$
\gamma^{(i)} = \frac{\hat{\gamma}^{(i)}}{\lVert x \rVert}
$$

An optimal margin classifier aims to find the parameters $w,b$ that maximise $\gamma$.

In other words, this means to find:

$$
\max_{w,b}\gamma \quad \text{s.t.} \quad \forall i \; \gamma^{(i)} \ge \gamma 
$$

This problem written like this cannot be solved with algorithms like gradient descend or similar, but can be rewritten in order to be optimized with one of those algorithms:

$$
\min_{w,b}\lVert x \rVert ^2\quad \text{s.t.} \quad \forall i \; \gamma^{(i)} \ge 0 
$$

## Kernels

Let's suppose that the parameter $w$ can be expressed as a linear combination between the training examples:

$$
w = \sum_{i=1}^n\alpha_iy^{(i)}x^{(i)} \quad \text{where} \quad x^{(i)} \in R^{k} \text{ with k very large}
$$

The Representer theorem prove that this is possible without loosing any performances.

- Assignments
    
    [Second Assignment 18 Oct → 17 Nov](https://www.notion.so/Second-Assignment-18-Oct-18-Nov-Grade-33-5-3908ec42f82447a58a5a058a5ff51a29?pvs=21)
    
    [First Assignment - 22 Sep → 20 Oct](Old%20stuff%2054864f9de49c44118cfc542766e8bc98/First%20Assignment%20-%2022%20Sep%20%E2%86%92%2020%20Oct%205c2803c0e86f4cd1ac872d2561505e0a.md)
    
- First Presentation
    
    Of course we want our model to have an high value of correct predictions, what we want more is for our model to have the lest amount of false negatives. This because in a sensitive environment such as the healthcare, we don’t want to predict that a person won’t have a stroke when they probably will. This means that the model should have an high recall value, without decreasing of course the accuracy.
    
- Final Presentation
    
    ### Original
    
    Since it was a simple classification problem, we started with creating a Logistic Regression based model. Instead of using a black-box model, we tried to implement it from scratch in order to have more control on its execution. We used gradient descent to reduce the cost and finally saw how the metrics changed, varying the threshold. Results were good but we wanted to try to get higher performances using other approaches. So we also implemented GDA (from scratch as well), K-Nearest Neighbors (with an efficient selection of the K value), Support Vector Machine and Random Forest. The last three were done using SkLearn.
    
    Putting all together, KNN with k=18 gives us the best accuracy with a lower recall. Logistic Regression works well too: choosing a threshold of 0.55 we managed to get a larger recall then KNN with a little lower accuracy. Random Forest (with a maxdepth of 5) and the Support Vector Classifier have more or less the same trend as logistic regression. Concerning our goal, GDA has the best performance since it has a high accuracy and a low number of false negatives.
    
    ### Reduced
    
    Since it was a simple classification problem, we started with Logistic Regression. We implemented it from scratch in order to have more control on its execution, seeing how the metrics changed varying the threshold.
    
    We then tried other methods like Gaussian Discriminant Analysis, from scratch as well, and others like K-Nearest Neihbors (with an optimal selection of the K value), Support Vector Machine and Random Forest using the SKLearn library.
    
    In conclusion we found that KNN with k=18 and RFC have the best accuracy but a low recall. Logistic Regression with threshold 0.55 and Support Vector Machine have a higher recall with a little lower accuracy, but concerning our goal GDA, in particular Quadratic Discriminant Analysis, has the highest recall, while maintaining high accuracy.