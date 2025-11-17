Bias in machine learning refers to systematic errors in a model's predictions that stem from either the training data or the algorithm itself.

1. **Sources of Bias**:
    
    - **Data Bias**: Occurs when the training data is not *representative of the real-world distribution*. For example, facial recognition systems trained on predominantly lighter-skinned individuals may underperform on darker-skinned individuals.
    - **Algorithmic Bias**: Arises from the *structure or design of the algorithm*, potentially leading to biased decisions regardless of the data.
    
2. **Types of Bias**:
    
    - **Selection Bias**: When the training data is not representative, such as in hiring models trained on past underrepresentation of certain groups.
    - **Implicit Bias**: Unintended biases due to feature selection or data collection methods, even without malicious intent.
    
3. **Detection and Mitigation**:
    
    - Techniques include preprocessing data to balance classes, applying fairness constraints during training, and post-processing steps.
    - Metrics like **precision, recall, F1 score,** and **AUC-ROC** can help identify biased performance across different groups.
