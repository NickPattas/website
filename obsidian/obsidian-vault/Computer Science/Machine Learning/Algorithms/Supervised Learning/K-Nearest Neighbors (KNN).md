The K-Nearest Neighbors (KNN) algorithm is a **supervised** machine learning technique used for both **classification and regression tasks.**

As a **classification algorithm**, KNN operates on the assumption that **similar data points are located near each other** and *can be grouped in the same category* based on their *proximity*.
### How KNN Works:

1. **Training Phase**: The model stores all training data points along with their corresponding labels or values.
   
2. **Prediction Phase**:
   
    - For a *new query point*, the algorithm *calculates the distance* to each stored training point using **a metric like Euclidean or Manhattan distance**.
    - It then **selects the K smallest distances, identifying the nearest neighbors.**
    - Depending on whether it's **classification or regression**:
        - **Classification**: The prediction is based on the *majority vote* of the K neighbors' labels.
        - **Regression**: The prediction is *the average* of the K neighbors' values.

### Key Considerations:

- **Choice of K**: A small K can lead to **sensitivity to noise**, while a large K may include more data points but could also **increase computational time**. There's a trade-off between bias and variance.
- **Preprocessing**: *Normalization or scaling* is often necessary to ensure that distance calculations are not skewed by feature scales.
- **Advantages**:
    - *Simple and effective* for many problems.
    - **No need for model training** beyond storing data.
- **Disadvantages**:
    - *Computationally intensive* with large datasets.
    - *Sensitive* to the scale of data and choice of K.
    - Prone to *the curse of dimensionality*, where distances become less meaningful in high dimensions.


## **Further Reading**

* [K-Nearest Neighbor(KNN) Algorithm](https://www.geeksforgeeks.org/k-nearest-neighbours/)
* [k_-nearest neighbors algorithm(Wiki)](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)
* [What is the k-nearest neighbors (KNN) algorithm?(IBM)](https://www.ibm.com/think/topics/knn)
