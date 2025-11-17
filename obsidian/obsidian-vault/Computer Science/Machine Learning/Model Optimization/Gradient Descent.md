 Gradient Descent is an `optimization algorithm` used in machine learning to *minimize some function by iteratively moving in the direction of steepest descent as defined by the negative gradient*. It is commonly used to train [[Neural Networks]], where it helps **adjust model weights** to *reduce prediction errors*.
 
Is a method for `unconstrained mathematical optimization`. It is a *first-order iterative algorithm for minimizing a differentiable multivariate function*.

A gradient simply measures the change in all weights with regard to the change in error. A gradient is a the slope of a function. The higher the gradient, the steeper the slope and the faster a model can learn. But if the slope is zero, the model stops learning. In mathematical terms, a gradient is a partial derivative with respect to its inputs.

The idea is to take *repeated steps in the opposite direction* of the gradient of the function at the current point, because this is the *direction of steepest descent*. Conversely, stepping in the direction of the gradient will lead to a trajectory that *maximizes that function*; the procedure is then known as **gradient ascent**.. Gradient descent should not be confused with [[Local Search Algorithms]], although both are iterative methods for optimization.

Similar to finding the line of best fit in [[Linear Regression]], the goal of gradient descent is to *minimize the cost function*, or the `error` between *predicted and actual $y$*. In order to do this, it requires two `data points`—a `direction` and a `learning rate`. These factors determine the *partial derivative calculations of future iterations*, allowing it to gradually arrive at the local or global minimum (i.e. point of convergence).

- **Learning rate** (also referred to as step size or the alpha) is the size of the steps that are taken **to reach the minimum**. This is typically a small value, and it is evaluated and updated based on the behavior of the cost function. High learning rates result in larger steps but risks *overshooting* the minimum. Conversely,**a low learning rate has small step sizes.** While it has the advantage of more precision, the number of iterations compromises overall efficiency as this takes more time and computations to reach the minimum.

- **The cost (or loss) function** measures the difference, or error, between actual y and predicted $y$ at its current position. This improves the machine learning model's efficacy by **providing feedback to the model** so that it can adjust the parameters to minimize the error and find the **local or global minimum**. It continuously iterates, moving along the direction of *steepest descent* (or the *negative gradient*) until the cost function is close to or at `zero`. At this point, the model will "stop learning". 

#### **A loss function refers to the error of one training example, while a cost function calculates the average error across an entire training set.**

![[Pasted image 20250519131707.png]]

Gradient descent is based on the observation that if the multi-variable function $F(x)$ is defined and differentiable in a neighborhood of a point $a$ , then $F(x)$ decreases fastest if one goes from $a$ in the direction of the negative gradient of $F$ at $a$ , − $∇ F ( a )$.
# $${\displaystyle \mathbf {a} _{n+1}=\mathbf {a} _{n}-\gamma \nabla F(\mathbf {a} _{n})}$$

for a small enough step size or learning rate γ∈$R_+$, then $F(a_n)≥F(a_{n+1})$.

In other words, the term $γ∇F(a)$ is subtracted from $a$ because we want to move against the gradient, toward the local minimum. With this observation in mind, one starts with a guess $x0$ for a local minimum of $F$, and considers the sequence $x0,x1,x2,…$ such that

$x_{n+1}$=$x_n−γ_n∇F(x_n)$, n≥0.

We have a monotonic sequence

$F(x0)≥F(x1)≥F(x2)≥⋯,$

so the sequence ($x_n$) converges to the desired local minimum. Note that the value of the step size $γ$ is allowed to change at every iteration.

It is possible to guarantee the convergence to a local minimum under certain assumptions on the function $F$ convex and $∇ F$ and particular choices of $γ$. Those include the sequence


$$ γ_{n}={\frac {\left|\left(\mathbf {x} _{n}-\mathbf {x} _{n-1}\right)^{T}\left[\nabla F(\mathbf {x} _{n})-\nabla F(\mathbf {x} _{n-1})\right]\right|}{\left\|\nabla F(\mathbf {x} _{n})-\nabla F(\mathbf {x} _{n-1})\right\|^{2}}}$$


### Types of gradient descent

There are three types of gradient descent learning algorithms: `batch gradient descent`, `stochastic gradient descent` and `mini-batch gradient descent`.

 ### Batch gradient descent

 Batch gradient descent, also called vanilla gradient descent, **sums the error for each point in a training set**, updating the model only after **all training examples have been evaluated**. This process referred to as a `training epoch`.

 While this batching provides *computation efficiency*, it can still have a *long processing time* for large training datasets as it still needs to store all of the data into memory. Batch gradient descent also usually **produces a stable error gradient and convergence**, but sometimes that convergence point isn’t the most ideal, finding the local minimum versus the global one.
 
 In general, it produces a *stable error gradient* and a *stable convergence*. But the stable error gradient can sometimes result in a **state of convergence that isn’t the best the model can achieve**. It also **requires the entire training dataset to be in memory** and available to the algorithm.

 #### *Slow but accurate*
 
 ### Stochastic gradient descent

 Stochastic gradient descent (SGD) **runs a training epoch for each example** within the dataset and it updates each training example's parameters one at a time. Since you only need to hold one training example, they are easier to store in memory. While these frequent updates can offer more detail and speed, **it can result in losses in computational efficiency when compared to batch gradient descent**. Its frequent updates can result in *noisy gradients*, but this can also be helpful in **escaping the local minimum and finding the global one**.

 #### *Faster but noisier*
 
 ### Mini-batch gradient descent

 Mini-batch gradient descent **combines concepts from both batch gradient descent and stochastic gradient descent**. It **splits the training dataset into small batch sizes** and performs *updates* on each of those batches. This approach strikes a *balance* between the computational efficiency of batch gradient descent and the speed of stochastic gradient descent.

 #### *Balanced speed and accuracy*
## **Further Reading**

* [Gradient Descent (Wiki)](https://en.wikipedia.org/wiki/Gradient_descent)
* [Gradient Descent Algorithm in Machine Learning](https://www.geeksforgeeks.org/gradient-descent-algorithm-and-its-variants/)
* [What is gradient descent?(IBM)](https://www.ibm.com/think/topics/gradient-descent#:~:text=Gradient%20descent%20is%20an%20optimization,between%20predicted%20and%20actual%20results.)
