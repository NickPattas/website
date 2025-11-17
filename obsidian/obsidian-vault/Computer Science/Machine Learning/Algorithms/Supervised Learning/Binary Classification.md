Binary classification is a supervised machine learning task where the model predicts one of two possible outcomes (classes) for a given input data point. It is one of the simplest forms of classification and is widely used in various applications such as spam detection, disease diagnosis, and customer churn prediction.

### Key Characteristics:

1. **Two Classes**: The output can only take on two values, typically labeled as `0` or `1`, representing "Negative" or "Positive", respectively.
2. **Supervised Learning**: The model is trained using labeled data, where each training example belongs to one of the two classes.

### Algorithms Used for Binary Classification:

1. [[Logistic Regression]]: Outputs probabilities between 0 and 1, which can be interpreted as the likelihood of an instance belonging to the positive class.
2. [[Support Vector Machines (SVM)]]: Finds a hyperplane in the feature space that best separates the two classes.
3. [[Decision Trees]]: Uses a tree-like structure to make decisions based on the features of the data.

### Evaluation Metrics:

- **Precision**: Ratio of correctly predicted positive instances to all predicted positive instances.
- **Recall (Sensitivity)**: Ratio of correctly predicted positive instances to all actual positive instances.
- **F1-Score**: Harmonic mean of precision and recall, providing a balanced measure of classification performance.
- **ROC-AUC**: Measures the ability of the model to distinguish between classes.

## Cross Entropy

**Binary cross-entropy (log loss)** quantifies the difference between the actual class labels (0 or 1) and the predicted probabilities output by the model. The lower the binary cross-entropy value, the better the model’s predictions align with the true labels.

Mathematically, Binary Cross-Entropy (BCE) is defined as:

$$BCE=-\frac{1}N​∑_{i=1}^N​[y_i​log(\hat{y_i}​)+(1−y_i​)log(1−\hat{y_i}​)]$$

* N is the number of samples in the dataset.}
* $y_i​$ is the actual binary label (0 or 1) of the ${i_{th}}$ sample.
* $\hat{y_i}$  is the predicted probability of the  $i^{th}$  sample belonging to the positive class.

Since the model’s output is a probability between 0 and 1, minimizing binary cross-entropy during training helps improve predictive accuracy, ensuring the model effectively distinguishes between two classes.

Binary Cross-Entropy measures the distance between the true labels and the predicted probabilities. When the predicted probability $p_i$ is close to the actual label $y_i$​, the BCE value is low, indicating a good prediction.

## Advantages

- Binary cross-entropy is differentiable with respect to the model’s predicted probabilities, making it suitable for gradient-based optimization algorithms such as stochastic gradient descent (SGD).
- It measures the information gain or loss between the predicted probabilities and the true labels, providing a quantitative measure of the model’s performance.
- Minimizing the binary cross-entropy loss during training aims to improve the model’s ability to correctly classify binary data and produce calibrated probability estimates.

## Disadvantages

- BCE can be sensitive to class imbalance, where one class significantly outnumbers the other. In such cases, the model may focus more on the majority class and perform poorly on the minority class. This imbalance can lead to biased predictions and decreased model performance.
- BCE is designed specifically for binary classification tasks and cannot be directly applied to multi-class classification problems without modification. In multi-class scenarios, alternative loss functions such as categorical cross-entropy are typically used.
- BCE loss can have optimization challenges when the model’s predicted probabilities are close to 0 or 1. In these cases, the logarithmic terms in the BCE formula can result in vanishing gradients, slowing down or hindering the training process. Techniques like label smoothing or clipping can help mitigate this issue.
- BCE treats each sample independently and computes the loss for each sample separately. This assumption may not hold true in some scenarios where samples are correlated or dependent on each other. For example, in sequence data or time series data, neighboring samples may exhibit dependencies that BCE does not capture.
- BCE does not directly account for misclassification costs or asymmetry between false positives and false negatives. In certain applications where the costs of different types of errors vary significantly, BCE may not adequately reflect the overall performance of the model.
- Like many loss functions, BCE can contribute to overfitting if not used in conjunction with appropriate regularization techniques or model architectures. Overfitting occurs when the model learns to memorize the training data rather than generalize to unseen data, leading to poor performance on new samples.


```python
import numpy as np
from keras.losses import binary_crossentropy

# Example true labels and predicted probabilities
y_true = np.array([0, 1, 1, 0, 1])
y_pred = np.array([0.1, 0.9, 0.8, 0.2, 0.7])

# Compute Binary Cross-Entropy using NumPy
def binary_cross_entropy(y_true, y_pred):
   bce = -np.mean(y_true * np.log(y_pred) + (1 - y_true) * np.log(1 - y_pred))
   return bce

bce_loss = binary_cross_entropy(y_true, y_pred)
print(f"Binary Cross-Entropy Loss (manual calculation): {bce_loss}")

# Compute Binary Cross-Entropy using Keras
bce_loss_keras = binary_crossentropy(y_true, y_pred).numpy()
print(f"Binary Cross-Entropy Loss (Keras): {bce_loss_keras}")
```


## **Further Reading** 

*  [Understanding binary cross-entropy / log loss](https://towardsdatascience.com/understanding-binary-cross-entropy-log-loss-a-visual-explanation-a3ac6025181a/)
