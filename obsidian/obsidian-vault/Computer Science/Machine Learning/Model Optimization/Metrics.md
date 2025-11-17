
# [[Linear Regression]]


 # MAE

Mean Absolute Error (MAE) is a statistical metric used to evaluate the accuracy of predictions by calculating the average absolute difference between predicted and actual values. It provides an interpretable measure of error in the same units as the data.

*  Equal weight to all the errors
*  Less sensitive to outliers

$$
\text{MAE} = \frac{1}{n} \sum_{i=1}^{n} |y_i - \hat{y}_i|  
$$
$$ \text{n = number of data points}$$
$$ y_i = \text{are the actual values}$$
$$\hat{y}_i = \text{the predicted values}$$


---

  # MSE

  Mean Squared Error (MSE) is a statistical metric used to evaluate the performance of regression models by quantifying the average squared difference between predicted and actual values.

  * Amplify larger errors
  * More sensitive to outliers

$$
\text{MSE} = \frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2
$$
   $$ \text{n = number of data points}$$
  $$ y_i = \text{are the actual values}$$
  $$\hat{y}_i = \text{the predicted values}$$

1. **Interpretation**: A lower MSE indicates better model performance since it means predictions are closer to actual values. However, MSE's units are squared, making interpretation less intuitive compared to Root Mean Squared Error (RMSE), which is the square root of MSE.
    
2. **Advantages**:
    
    - Provides a clear measure of error magnitude.
    - Emphasizes larger errors due to squaring, highlighting model weaknesses.
3. **Disadvantages**:
    - Sensitive to outliers, as squared errors amplify large discrepancies.
    - Less interpretable without context or comparison to baseline models.


---

 # RMSE

Root Mean Squared Error (RMSE) is a statistical measure that quantifies the average magnitude of the errors in a set of predictions. It is calculated by taking the square root of the Mean Squared Error (MSE), which helps to convert the squared differences back into the original units of the data, making it more interpretable.

* Dependent variable

$$
\text{RMSE} = \sqrt{\frac{1}{n}\sum_{i=1}^{n}(y_i - \hat{y}_i)^2}
$$
$$ \text{n = number of data points}$$ $$ y_i = \text{are the actual values}$$$$\hat{y}_i = \text{the predicted values}$$

1. **Interpretation**: Since RMSE is in the same units as the data, it provides a direct sense of how far off the predictions are on average. A lower RMSE indicates better model performance.
    
2. **Relation to MSE**: RMSE is the square root of MSE, which means while MSE gives an idea of error magnitude squared, RMSE provides the actual error magnitude in original units.
    
3. **Sensitivity to Outliers**: Like MSE, RMSE is sensitive to outliers because squaring errors (as done in MSE) magnifies larger discrepancies. This sensitivity can be both a strength and a weakness depending on the context.


# [[Logistic Regression]]

 # Accuracy
 
  $$\text{Accuracy} = \frac{\text{Number of Correct Predictions}}{\text{Total Number of Predictions}}$$

---

 # Precision
 
  $$\text{Accuracy} = \frac{TP}{TP + FP}$$

  Based on *Confusion Matrix 
  - TP = True Positives
  - FP = False Positives

---
 
 # Recall

  $$ Recall = \frac{TP}{TP + FN}$$

  Based on *Confusion Matrix 
  - TP = True Positives
  - FN = False Negatives

 ---
 
 # F1 - Score

  Combination of Precision and Recall

  $$\frac{2TP}{2TP + FP + FN}$$

  Based on *Confusion Matrix 
  - TP = True Positives
  - FP = False Positives
  - FN = False Negatives

---
 
 # ROC

  ROC stands for **Receiver Operating Characteristic** in machine learning. It is a graphical tool used to evaluate the performance in [[Binary Classification]]. The ROC curve plots the **true positive rate (TPR)** against the **false positive rate (FPR)** at various threshold settings.
 
  The area under the ROC curve (AUC) is a key metric that provides an aggregate measure of the model's ability to distinguish between classes. A higher AUC indicates better performance, with perfect separation achieving an AUC of 1.