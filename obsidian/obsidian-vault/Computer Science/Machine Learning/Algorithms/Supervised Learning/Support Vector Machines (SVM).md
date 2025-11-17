A Support Vector Machine (SVM) is a **supervised machine learning algorithm** used for both **classification and regression tasks**. It works by finding the *optimal hyperplane* (a line in 2D, a plane in 3D, or a higher-dimensional space) that separates different classes with the largest margin. **This hyperplane, along with the closest data points (support vectors), defines the decision boundary**. 

In addition to performing *linear classification*, SVMs can efficiently perform *non-linear classification* using the kernel trick, representing the data only through a set of pairwise similarity comparisons between the original data points using a *kernel function*, which **transforms them into coordinates in a higher-dimensional feature space**. Thus, SVMs use the kernel trick to implicitly **map their inputs into high-dimensional feature spaces, where linear classification can be performed.**

Being *max-margin models*, SVMs are **resilient to noisy data** (e.g., misclassified examples). SVMs can also be used for regression tasks, where the objective becomes ϵ-sensitive.

### Support Vector Machine (SVM) Terminology

- **Hyperplane:** A **decision boundary separating different classes** in **feature space**, represented by the equation $wx + b = 0$ in linear classification.
- **Support Vectors**: The **closest data points to the hyperplane**, crucial for determining the hyperplane and margin in SVM.
- **Margin**: The **distance between the hyperplane and the support vectors**. SVM aims to **maximize this margin for better classification performance**.
- **Kernel:** **A function that maps data to a higher-dimensional space**, enabling SVM to handle non-linearly separable data.
- **Hard Margin**: A maximum-margin hyperplane that **perfectly separates the data without misclassifications**.
- **Soft Margin**: Allows some **misclassifications by introducing slack variables**, balancing margin maximization and misclassification **penalties** when data is not perfectly separable.
- **C**: A regularization term balancing margin maximization and misclassification penalties. **A higher C value enforces a stricter penalty for misclassifications**.
- **Hinge Loss**: A **loss function penalizing** misclassified points or margin violations, combined with regularization in SVM.
- **Dual Problem**: Involves solving for **Lagrange multipliers** associated with support vectors, facilitating the kernel trick and efficient computation.

### How does Support Vector Machine Algorithm Work?

The key idea behind the SVM algorithm is to find the hyperplane that best separates two classes by maximizing the margin between them. This margin is the distance from the hyperplane to the nearest data points (**support vectors**) on each side.

![Multiple hyperplanes separating the data from two classes](https://media.geeksforgeeks.org/wp-content/uploads/20201211181531/Capture.JPG)
 *Multiple hyperplanes separate the data from two classes*

The best hyperplane, also known as the **"hard margin,"** is the one that **maximizes the distance between the hyperplane and the nearest data points from both classes**. This ensures a **clear separation** between the classes.

___
### Advantages of Support Vector Machine (SVM)

1. **High-Dimensional Performance**: SVM excels in high-dimensional spaces, making it suitable for [[Image Classification 1]] and **Gene Expression Analysis**.
2. **Nonlinear Capability**: Utilizing **kernel functions** like **RBF** and **polynomial**, SVM effectively handles **nonlinear relationships**.
3. **Outlier Resilience**: The **soft margin** feature allows SVM to ignore outliers, enhancing robustness in **spam detection** and **anomaly detection**.
4. **Binary and Multiclass Support**: SVM is effective for both **binary classification** and **multiclass classification**, suitable for applications in **text classification**.
5. **Memory Efficiency**: SVM focuses on **support vectors**, making it memory efficient compared to other algorithms.

### Disadvantages of Support Vector Machine (SVM)

1. **Slow Training**: SVM can be slow for large datasets, affecting performance in **SVM in data mining** tasks.
2. **Parameter Tuning Difficulty**: Selecting the right **kernel** and adjusting parameters like **C** requires careful tuning, impacting **SVM algorithms**.
3. **Noise Sensitivity**: SVM struggles with noisy datasets and overlapping classes, limiting effectiveness in real-world scenarios.
4. **Limited Interpretability**: The complexity of the **hyperplane** in higher dimensions makes SVM less interpretable than other models.
5. **Feature Scaling Sensitivity**: Proper **feature scaling** is essential; otherwise, SVM models may perform poorly.

---
### Mathematical Computation: SVM
The equation for the linear hyperplane can be written as:

$$w^Tx+b=0$$

Where:

- $w$ is the **normal vector** to the hyperplane (the **direction perpendicular to it**).
- $b$ is the **offset or bias term**, representing the **distance of the hyperplane from the origin along the normal vector $w$**.
### Distance from a Data Point to the Hyperplane

The distance between a data point $x_i$ and the decision boundary can be calculated as:

$$di=\frac{w^Tx_i+b}{||w||}$$


where ||w|| represents the Euclidean norm of the weight vector w. Euclidean norm of the normal vector W

### Linear SVM Classifier

Distance from a Data Point to the Hyperplane:

$$ \hat{y} = \begin{cases} 1:  w^Tx + b \geq 0 \\ 0 :  w^Tx + b < 0\end{cases} $$

Where $\hat{y}$​ is **the predicted label of a data point**.

### Optimization Problem for SVM

For a linearly separable dataset, the goal is to find the hyperplane that maximizes the margin between the two classes while ensuring that all data points are correctly classified. This leads to the following optimization problem:

minimize​$\frac{1}{2}$​$||w||^2$

Subject to the constraint:

$$y_i(w^Tx_i+b)≥1 \text{ for } i=1,2,3,⋯,m$$

Where:

- $y_i$ is the class label (+1 or -1) for each training instance.
- $x_i$ is the feature vector for the $i$-th training instance.
- $m$ is the total number of training instances.

The condition $y_i(w^Tx_i+b)≥1$ ensures that each data point is correctly classified and lies outside the margin.

### Soft Margin Linear SVM Classifier

In the presence of outliers or non-separable data, the SVM allows some misclassification by introducing slack variables ζiζi​​. The optimization problem is modified as:

minimize​$\frac{1}{2}$​$||w||^2$ + $C\sum_{i=1}^{m}{​ζ_i}​$

Subject to the constraints:

$y_i(w^Tx_i+b)≥1$ − $ζ_i$  and  $ζ_i≥0$ for $i=1,2,…,m$

Where:

- $C$ is a regularization parameter that controls the trade-off between margin maximization and penalty for misclassifications.
- $ζ_i$​​ are slack variables that represent the degree of violation of the margin by each data point.

### Dual Problem for SVM

The dual problem involves maximizing the Lagrange multipliers associated with the support vectors. This transformation allows solving the SVM optimization using kernel functions for non-linear classification.

The dual objective function is given by:

$$maximize\frac{1}{2}\sum_{i=1}^{m}\sum_{j=1}^{m}{a_ia_jt_it_jK(x_ix_j)}-\sum_{i=1}^{m}{a_i}$$

Where:

- $α_i$ are the** Lagrange multipliers** associated with the $i$-th training sample.
- $t_i$ is the class label for the $i$-th training sample (+1+1+1 or −1-1−1).
- $K(x_i,x_j)$ is the kernel function that computes the similarity between data points $x_i$​​ and $x_j$. **The kernel allows SVM to handle non-linear classification problems by mapping data into a higher-dimensional space**.

The dual formulation optimizes the Lagrange multipliers αiαi​​, and the support vectors are those training samples where $α_i>0$.

### SVM Decision Boundary

Once the dual problem is solved, the decision boundary is given by:

$$w=\sum_{i=1}^{m}{a_it_iK(x_ix)+b}$$

Where $w is the weight vector, $x$ is the test data point, and bb is the bias term.

Finally, the bias term $b$ is **determined by the support vectors**, which satisfy:

$$t_i(w^Tx_i−b)=1⇒b=w^Tx_i−t_i​$$

Where $x_i$​​ is any support vector.

---
### Types of Support Vector Machine

Based on the nature of the decision boundary, Support Vector Machines (SVM) can be divided into **two main parts**:

- **Linear SVM:** Linear SVMs use a **linear decision boundary to separate the data points of different classes**. When the data can be precisely linearly separated, linear SVMs are very suitable. This means that a single straight line (in 2D) or a hyperplane (in higher dimensions) can entirely divide the data points into their respective classes. A hyperplane that maximizes the margin between the classes is the *decision boundary*.

- **Non-Linear SVM:** Non-Linear SVM can be used to classify data when it cannot be separated into two classes by a straight line (in the case of 2D). By using kernel functions, nonlinear SVMs can handle nonlinearly separable data. The original input data is transformed by these kernel functions into a higher-dimensional feature space, where the data points can be linearly separated. A linear SVM is used to locate a nonlinear decision boundary in this modified space.

### Python Implementation

```python
from sklearn.datasets import load_breast_cancer
import matplotlib.pyplot as plt
from sklearn.inspection import DecisionBoundaryDisplay
from sklearn.svm import SVC

# Load the datasets
cancer = load_breast_cancer()
X = cancer.data[:, :2]
y = cancer.target

#Build the model
svm = SVC(kernel="rbf", gamma=0.5, C=1.0)
# Trained the model
svm.fit(X, y)

# Plot Decision Boundary
DecisionBoundaryDisplay.from_estimator(
        svm,
        X,
        response_method="predict",
        cmap=plt.cm.Spectral,
        alpha=0.8,
        xlabel=cancer.feature_names[0],
        ylabel=cancer.feature_names[1],
    )

# Scatter plot
plt.scatter(X[:, 0], X[:, 1], 
            c=y, 
            s=20, edgecolors="k")
plt.show()
```

**Output**:
![Breast Cancer Classifications with SVM RBF kernel-Geeksforgeeks](https://media.geeksforgeeks.org/wp-content/uploads/20230518114226/download-(36).png)
*Breast Cancer Classifications with SVM RBF kernel*

## **Further Reading**

* [Support vector machine (Wiki)](https://en.wikipedia.org/wiki/Support_vector_machine)
* [Support Vector Machine (SVM) Algorithm](https://www.geeksforgeeks.org/support-vector-machine-algorithm/)