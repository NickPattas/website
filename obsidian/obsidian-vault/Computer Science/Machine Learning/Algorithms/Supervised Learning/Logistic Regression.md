Logistic Regression is a fundamental statistical method used in data science for classification problems, particularly when the dependent variable is binary (e.g., yes/no, success/failure). It predicts the probability of an event occurring by fitting a logistic function to the data. The logistic function maps any input value to a probability between `0` and `1`, making it suitable for predicting probabilities.

The basic form of the logistic regression equation is:
 # $$P(y=1) = \frac{e^{\beta_0 + \beta_1 x}}{1 + e^{\beta_0 + \beta_1 x}}$$
The beta values, β₀ and β₁, are coefficients that define the relationship between the independent variable (x) and the probability of the outcome (y=1).

- **β₀ (Intercept)**: This is the log-odds of the event occurring when (x = 0). It represents the baseline effect when no predictor variables are considered.
- **β₁ (Slope)**: This coefficient indicates how much the log-odds of (y=1) change for each one-unit increase in (x), holding all other variables constant.

Unlike [[Linear Regression]], which can produce values outside the `0-1` range, logistic regression ensures predictions are within this interval.

There are three types of logistic regression:

1. **Binary**: For two possible outcomes.
2. **Multinomial**: For more than two outcomes.
3. **Ordinal**: When categories are ordered.

Model evaluation is done using [[Metrics]] like accuracy, precision, recall, F1-score, and ROC-AUC. Regularization techniques such as Lasso and Ridge can prevent overfitting by adding penalties to the loss function based on coefficient sizes.

Training involves maximum likelihood estimation, which iteratively adjusts coefficients to maximize the probability of observing the data. Feature engineering is crucial for model performance, and interpreting coefficients helps understand feature influence.


```python
import numpy as np

from sklearn.model_selection import train_test_split

from sklearn import datasets

class LogisticRegression:

  def __init__(self, lr=0.001, n_iters=1000):

    self.lr = lr

    self.n_iters = n_iters

    self.weights = None

    self.bias = None

  

  def sigmoid(self, z):

    return 1 / (1 + np.exp(-z))

  

  def cost_function(self, h, y):

    return (-y * np.log(h) + (1-y) * np.log(1-h)).mean()

  

  def fit(self, X, y):

    n_samples, n_features = X.shape

    self.weights = np.zeros(n_features)

    self.bias = 0

  

    for _ in range(self.n_iters):

      linear_pred = np.dot(X, self.weights) + self.bias

      predictions = self.sigmoid(linear_pred)

  

      gw = np.dot(X.T, (predictions - y)) / n_samples

      gb = np.sum(predictions - y) / n_samples

  

      self.weights -= self.lr * gw

      self.bias -= self.lr * gb

  

    final_z = np.dot(X, self.weights) + self.bias

    final_h = self.sigmoid(final_z)

    final_cost = self.cost_function(final_h, y)

    return final_cost

  

  def predict(self, X, threshold=0.5):

    linear_pred = np.dot(X, self.weights) + self.bias

    predictions = self.sigmoid(linear_pred)

    class_pred = [0 if y <= threshold else 1 for y in predictions]

    return class_pred

if __name__ == "__main__":

  bc = datasets.load_breast_cancer()

  X, y = bc.data, bc.target

  X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=101)

  classification_model = LogisticRegression(lr=0.01)

  classification_model.fit(X_train, y_train)

  y_pred = classification_model.predict(X_test)
  

  def accuracy(y_pred, y_test):

    return np.sum(y_pred == y_test) / len(y_test)


  print(f"Accuracy: {accuracy(y_pred, y_test)}")
```

Example Projects:

![[ScikitLearn_Logistic_Regression.ipynb]]
![[Breast_Cancer_Prediction.ipynb]]
