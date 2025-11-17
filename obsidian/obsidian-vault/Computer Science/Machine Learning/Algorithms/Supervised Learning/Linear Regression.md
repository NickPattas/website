# $$y = mx + b$$
 # $$m =\frac{\sum_{n}(x_i-\overline{x})(x_i-\overline{y})}{\sum_{n}(x_i-\overline{x})^2}$$
 m = slope
 b = vertical shift
 x  = input

**Model Objective:**  
The goal is to find the best-fitting line that minimizes the sum of squared differences between observed and predicted values, using ordinary least squares.

It **predicts** an outcome (dependent variable) based on one or more predictors (independent variables), assuming a ***straight-line relationship**.

**Types of Linear Regression:**

1. **Simple Linear Regression:** Involves one predictor variable.
2. **Multiple Linear Regression:** Involves two or more predictor variables

Simple Linear Regression
```python
x_values = [i for i in range(0, 200)]
y_values = [i for i in range(0,400,2)]

def mean(values):
  return sum(values)/float(len(values))

mean_x = mean(x_values)
mean_y = mean(y_values)

def covariance(x, mean_x, y, mean_y):
  cov = 0
  for i in range(len(x)):
    cov += (x[i] - mean_x)*(y[i] - mean_y)
  return cov

def variance(values, mean_value):
  var = 0
  for i in range(len(values)):
    var += (values[i] - mean_value) ** 2
  return var

def coefficients(x, mean_x, y, mean_y):
  m = covariance(x, mean_x, y, mean_y) / variance(x, mean_x)
  b = mean_y - m * mean_x
  return m, b

slope, intercept = coefficients(x_values, mean_x, y_values, mean_y)

def simple_linear_regression(x, slope, intercept):
  return slope * x + intercept

user_input = int(input("Enter a number: "))
prediction = simple_linear_regression(user_input, slope, intercept)
print(prediction)
```


Multiple Linear Regression
![[Car_Price_Prediction.ipynb]]
![[Hero_Win_Rate.ipynb]]
