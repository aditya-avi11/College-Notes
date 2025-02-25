
Margin maximization is a fundamental concept in Support Vector Machines (SVM). The **margin** refers to the distance between the separating hyperplane (decision boundary) and the closest data points from each class, known as **support vectors**. SVM aims to find the hyperplane that maximizes this margin, as a larger margin leads to better generalization on unseen data.

### Mathematical Formulation of SVM

#### 1. **Hyperplane Equation**:
In an SVM, the hyperplane that separates two classes in an \( n \)-dimensional space is defined by:

	$\mathbf{w}^T \mathbf{x} + b = 0$

Where:
-  **w** is the normal vector to the hyperplane.
-  **x** is the input vector (data point).
- **b** is the bias term (offset).

The goal is to find **w** and **b** that define the optimal hyperplane.

#### 2. **Classification Condition**:
For a binary classification problem where the labels are $\( y_i \in \{-1, +1\} \)$, the decision boundary should classify data points such that:


$y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1$

This condition ensures that all points are classified correctly, with a margin of at least 1 on either side of the hyperplane.

#### 3. **Distance to the Hyperplane**:
The perpendicular distance of any point $\mathbf{x}$ \ from the hyperplane is given by:


$\text{Distance} = \frac{| \mathbf{w}^T \mathbf{x} + b |}{\| \mathbf{w} \|}$


For support vectors (the points closest to the hyperplane), this distance is exactly  $1 / \| \mathbf{w} \|$ .

#### 4. **Margin Maximization**:
The margin is defined as twice the distance from the hyperplane to the nearest support vectors, which is:


$$
\text{Margin} = \frac{2}{\| \mathbf{w} \|}
$$


To maximize the margin, we need to minimize  $\| \mathbf{w} \|$  subject to the constraint that the classification condition holds for all data points, i.e.,  $y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1$ .

#### 5. **Optimization Problem**:
Maximizing the margin is equivalent to minimizing  $\frac{1}{2} \| \mathbf{w} \|^2$  (the factor  $\frac{1}{2}$  is for mathematical convenience) subject to the constraints. This leads to the following optimization problem:


$\min_{\mathbf{w}, b} \frac{1}{2} \| \mathbf{w} \|^2$

**subject to:**

$y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1, \quad \forall i$


This is a **convex optimization problem** that can be solved using methods like Lagrange multipliers and quadratic programming.

#### 6. **Soft Margin for Non-separable Data**:
In real-world data, perfect separation may not always be possible, so SVM introduces a **soft margin** that allows some misclassification. The optimization problem is modified by introducing **slack variables**  $\xi_i$  to allow violations of the margin:


$\min_{\mathbf{w}, b, \xi} \frac{1}{2} \| \mathbf{w} \|^2 + C \sum_{i=1}^{n} \xi_i$

**subject to:**

$y_i (\mathbf{w}^T \mathbf{x}_i + b) \geq 1 - \xi_i, \quad \xi_i \geq 0, \quad \forall i$


Here:
-  $\xi_i$  measures how much the  $i$ -th data point violates the margin.
-  $C$  is a regularization parameter that controls the trade-off between maximizing the margin and allowing some misclassification (a higher \( C \) penalizes misclassification more).

### Dual Formulation

The optimization problem can also be expressed in its **dual form**, where the problem is expressed in terms of Lagrange multipliers \( \alpha_i \). The dual form is particularly useful for applying the **kernel trick** to deal with non-linear data.

The dual problem is:
$$
$\max_{\alpha} \sum_{i=1}^{n} \alpha_i - \frac{1}{2} \sum_{i=1}^{n} \sum_{j=1}^{n} \alpha_i \alpha_j y_i y_j \mathbf{x}_i^T \mathbf{x}_j$
$$
subject to:

$$ $\sum_{i=1}^{n} \alpha_i y_i = 0, \quad 0 \leq \alpha_i \leq C, \quad \forall i$ $$


Here, \( \alpha_i \) are the Lagrange multipliers, and only non-zero  $\alpha_i$  correspond to the support vectors.

### Summary of Margin Maximization

- **Objective**: Maximize the margin  $\frac{2}{\| \mathbf{w} \|}$ , which leads to better generalization.
- **Formulation**: Minimize $\frac{1}{2} \| \mathbf{w} \|^2$ , subject to the classification constraints.
- **Soft Margin**: Allows for some margin violations using slack variables $\xi_i$ , controlled by a parameter \( C \).
- **Dual Problem**: Solves the optimization problem using Lagrange multipliers, enabling the use of kernel functions for non-linear data.

This approach to maximizing the margin is what makes SVM a powerful classifier, particularly for high-dimensional and complex datasets.


<hr>
<hr>

## Hyperplane Equation

In the equation of the hyperplane, $\mathbf{w}^T \mathbf{x} + b = 0$, the term $\mathbf{w}^T$ refers to the **transpose** of the weight vector $\mathbf{w}$, and $\mathbf{w}^T \mathbf{x}$ represents the **dot product** between the weight vector $\mathbf{w}$ and the input vector $\mathbf{x}$.

### What is $\mathbf{w}^T \mathbf{x}$?

1. **Weight vector** $\mathbf{w}$:
   - This is a vector of coefficients that define the orientation of the hyperplane in the feature space.
   - If $\mathbf{x}$ has $n$ features (dimensions), then $\mathbf{w}$ is also an $n$-dimensional vector. Each element in $\mathbf{w}$ corresponds to a weight assigned to the respective feature of $\mathbf{x}$.

2. **Transpose $\mathbf{w}^T$**:
   - The transpose of a vector turns a column vector into a row vector, or vice versa. In this case, $\mathbf{w}^T$ turns the column vector $\mathbf{w}$ into a row vector, allowing it to be multiplied by the input vector $\mathbf{x}$.

3. **Dot product** $\mathbf{w}^T \mathbf{x}$:
   - The dot product of two vectors is the sum of the products of their corresponding components. Mathematically:
   $$
   \mathbf{w}^T \mathbf{x} = w_1 x_1 + w_2 x_2 + \dots + w_n x_n
   $$
   
   where $w_1, w_2, \dots, w_n$ are the components of the weight vector $\mathbf{w}$, and $x_1, x_2, \dots, x_n$ are the components of the input vector $\mathbf{x}$.

### Example

Let's consider a simple example with a 2-dimensional input vector (i.e., 2 features):

- Suppose $\mathbf{x} = [x_1, x_2]$ is the input vector, where:
  $$
  \mathbf{x} = \begin{bmatrix} 2 \\ 3 \end{bmatrix}
  $$
  So, $x_1 = 2$ and $x_2 = 3$.

- Let $\mathbf{w} = [w_1, w_2]$ be the weight vector, where:
  $$
  \mathbf{w} = \begin{bmatrix} 1 \\ -1 \end{bmatrix}
  $$
  So, $w_1 = 1$ and $w_2 = -1$.

- The **transpose** $\mathbf{w}^T$ is:
  $$
  \mathbf{w}^T = \begin{bmatrix} 1 & -1 \end{bmatrix}
  $$

- Now, the dot product $\mathbf{w}^T \mathbf{x}$ is calculated as:
  $$
  \mathbf{w}^T \mathbf{x} = (1)(2) + (-1)(3) = 2 - 3 = -1
  $$

So, $\mathbf{w}^T \mathbf{x} = -1$ in this case.

### Hyperplane Equation

If we include the bias term $b$ in the equation of the hyperplane, it becomes:

$$
\mathbf{w}^T \mathbf{x} + b = 0
$$

Assume $b = 2$, then:

$$
-1 + 2 = 1
$$

This means the point $\mathbf{x} = [2, 3]$ does not lie on the hyperplane since $\mathbf{w}^T \mathbf{x} + b \neq 0$. If the result were zero, it would indicate that the point is exactly on the hyperplane.

### Summary

- $\mathbf{w}^T$ is the **transpose** of the weight vector $\mathbf{w}$, turning a column vector into a row vector.
- The term $\mathbf{w}^T \mathbf{x}$ is the **dot product** of the weight vector $\mathbf{w}$ and the input vector $\mathbf{x}$, calculated by summing the products of their corresponding elements.
- The equation $\mathbf{w}^T \mathbf{x} + b = 0$ defines the hyperplane, where $b$ is the bias or intercept that shifts the hyperplane.