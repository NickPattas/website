## The Function
 
The sigmoid function is a mathematical function with an S-shaped curve, often denoted as σ(x). It maps any real number to a value between `0` and `1`, making it useful for binary classification tasks where probabilities are needed. The function is defined by the formula:
# $$
σ(χ) = \frac{1}{1+e^{(-z)}}
$$
## Key Properties:

- **S-shaped Curve**: The sigmoid function starts increasing slowly, accelerates in the middle, and then levels off.
- **Output Range**: It outputs values between 0 and 1, which is ideal for converting model predictions into probabilities.
- **Derivative**: The derivative of the sigmoid function is σ'(x) = σ(x)(1 - σ(x)), which is useful during backpropagation but can lead to vanishing gradients when inputs are far from zero.

### Applications:

- [[Binary Classification]]: Used in [[logistic regression]] and neural networks to output probabilities.
- [[Neural Networks]]: Often used in the output layer for binary classification tasks, though less common in hidden layers due to vanishing gradient issues.

### Limitations:

- **Vanishing Gradients**: The derivative becomes very small for inputs far from zero, which can slow down training in deep networks.
- **Alternatives**: Functions like tanh and ReLU are sometimes preferred for hidden layers to mitigate these issues.
