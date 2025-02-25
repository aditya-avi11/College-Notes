![[Pasted image 20241002130133.png]]

## Kernel Tricks in SVM

**Kernel tricks** are used in Support Vector Machines (SVM) to solve non-linearly separable problems by transforming the data into a higher-dimensional space, where a linear decision boundary can be applied. The goal is to compute the transformation efficiently using a kernel function that calculates the dot product in the transformed space directly.

### 1. Linear Kernel
- **Formula**: `K(x, y) = x · y`
- **Usage**: Suitable for linearly separable data.
- **When to use**: When data can be separated by a straight line (or hyperplane). Works well with high-dimensional data.
- **Example**: Text classification where the feature space is sparse but high-dimensional.

### 2. Polynomial Kernel
- **Formula**: `K(x, y) = (x · y + c)^d`
- **Usage**: Maps data into a higher-degree polynomial space to enable complex decision boundaries.
- **Parameters**:
  - `d` is the degree of the polynomial (controls complexity).
  - `c` is a constant that controls the trade-off between higher and lower-degree terms.
- **When to use**: For data with complex interactions or polynomial patterns.
- **Example**: Data that follows quadratic or cubic patterns (e.g., polynomial regression).

### 3. Radial Basis Function (RBF) / Gaussian Kernel
- **Formula**: `K(x, y) = exp(-γ ||x - y||^2)`
- **Usage**: Maps data into an infinite-dimensional space. Effective for complex non-linear boundaries.
- **Parameter**:
  - `γ` controls the width of the Gaussian (higher values create more localized boundaries).
- **When to use**: When data has non-linear relationships and circular or elliptical decision boundaries are expected.
- **Example**: Image classification, handwriting recognition.

### 4. Sigmoid Kernel
- **Formula**: `K(x, y) = tanh(α x · y + c)`
- **Usage**: Resembles neural network activation functions, used for mapping non-linear data.
- **Parameters**:
  - `α` and `c` are constants that control the decision boundary shape.
- **When to use**: Historically used to simulate neural network behavior, but less common now.
- **Example**: Neural network-like tasks (rarely used nowadays).

### 5. Custom Kernels
- **Usage**: Define a custom kernel based on domain knowledge.
- **When to use**: When specific transformations or applications require it, like string matching or graph kernels.
- **Example**: Biological sequence comparison, graph data processing.

---

## Applying Kernel Functions in Python

You can use different kernel functions in SVMs with `scikit-learn` using the `SVC` class:

```python
from sklearn import svm

# Linear Kernel
clf_linear = svm.SVC(kernel='linear')
clf_linear.fit(X_train, y_train)

# Polynomial Kernel
clf_poly = svm.SVC(kernel='poly', degree=3, coef0=1)
clf_poly.fit(X_train, y_train)

# RBF Kernel
clf_rbf = svm.SVC(kernel='rbf', gamma=0.5)
clf_rbf.fit(X_train, y_train)

# Sigmoid Kernel
clf_sigmoid = svm.SVC(kernel='sigmoid', coef0=1)
clf_sigmoid.fit(X_train, y_train)
```


<hr><hr>

### When to Use Which Kernel

- **Linear Kernel**: Use when data is linearly separable or the number of features is high relative to the number of samples.
- **Polynomial Kernel**: Use when you expect interactions between features and when data has polynomial relationships (non-linear but smooth).
- **RBF Kernel**: Default choice for non-linear SVMs, works well when data has complex boundaries that are not easily separated by polynomials.
- **Sigmoid Kernel**: Use when you want behavior similar to a neural network. It's less common nowadays.

Each kernel comes with its own parameters (degree, gamma, etc.), so cross-validation is important to tune these hyperparameters for optimal performance.