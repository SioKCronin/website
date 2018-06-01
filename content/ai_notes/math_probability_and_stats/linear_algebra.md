---
title: Linear Algebra Basics
menu:
    ai_notes:
        parent: Math, Probability & Stats
---
## Useful terms and ideas

* **diagonal matrix**: Matrix with zero values except on the diagonal.
* **change of basis matrix**: Taking the product of this matrix provides a new basis,
which is helpful to us if that basis transformation sets us up for an operation
that requires the matrix to be in a particular form. For instance, a change of basis
matrix could diagonalize the matrix, such as the choice of the orthogonal matrix
as the change of basis matrix in PCA. 
* **eigen values**: These are the lambda values that satisfy the following equation
where A is our input data, and x is the eigenvector: $A x = \lambda x$.
* **eigen vectors (characteristic vector)**: In a linear transformation, $L(x)$,
then $x$ is an eigenvalue of $L()$ if $L(x)$ is a scalar multiple of $x$. 
* **eigen decomposition**: This is when we take a matrix, and define it as a product of
$Q^{T}DQ$ where $Q$ is an orthogonal matrix, and and $D$ is the diagonal matrix of eigenvalues.
The magic is that the columns of $Q$ are the principal components of our matrix! The way 
to think about this is that for the covariance matrix $S\_{x} = \frac{1}{m}X^{T}X$,
where X is our input matrix, if we transform our matrix to $S\_{y}$, which will be a diagonal 
matrix where $S\_{y} = \frac{1}{m}Y^TY = P^TS\_{x}P$ (since we can substite Y = XP, 
where $P$ is our change of basis matrix), and select $Q$ (the orthogonal matrix) as our $P$ 
(oh so handy!), then we get $S\_{y} = Q^TS\_{x}Q = Q^T(QDQ^T)Q = D$, and the columns of
$D$ are our principal components because they equal the columns of $S\_{y}$ which is our covariance
matrix where all feature products are zero except the products of the features and themselves,
which means we have reduced rudancy of signal to zero!
* **matrix transformations** include *reflection*, *orthogonal projection*, *rotation*,
*compression*, and *shearing*. 
* Because they are so useful, you can choose your eigenvectors as your basis (eigenbasis),
provided they span your space
* In 1751, Leonhard Euler proved that any body has a principal axis of rotation. 

## Scipy example

We are entering three pies into the bakeoff, and want to make sure we win.
We've tried a lot of different ingredients, but ultimatley have found that taste 
comes down to **butter**, **salt**, **sugar**, and **grandma's secret spice blend**. 

```python
import scipy.linalg as la
import numpy as np
```

```python
w = 1 #tbl_of_butter
x = 1 #dash_of_salt
y = 1 #spoonful_of_sugar
z = 1 #undisclosed_measurement_of_spice

pie1 = 3*w + 5*x + 30*y + 10*z
pie2 = 2*w + 3*x + 40*y + 15*z
pie3 = 4*w + 2*x + 10*y + 30*z
pie4 = 10*w + 2*x + 10*y + 30*z
```

```python
A = np.array([[3,5,30,10],[2,3,40,15],[4,2,10,30], [10,2,10,30]])
```

```python
A
```
    array([[ 3,  5, 30, 10],
           [ 2,  3, 40, 15],
           [ 4,  2, 10, 30],
           [10,  2, 10, 30]])

```python
inv = la.inv(A)
```

    array([[ 4.20539024e-19,  3.48136945e-18, -1.66666667e-01,
             1.66666667e-01],
           [ 3.55932203e-01, -2.71186441e-01,  1.15819209e-01,
            -9.88700565e-02],
           [-2.03389831e-02,  4.40677966e-02, -2.09039548e-02,
             5.64971751e-03],
           [-1.69491525e-02,  3.38983051e-03,  5.48022599e-02,
            -1.75141243e-02]])

## TEST

```python
A = np.array([[2, 3, -1], [1, -1, 0], [0, 5, 2], [3, 2, 1]])
```

```python
A
```
    array([[ 2,  3, -1],
           [ 1, -1,  0],
           [ 0,  5,  2],
           [ 3,  2,  1]])

```python
test1 = np.array([2, 3, -7, 3])
test2 = np.array([0, 0, 0, 0])
test3 = np.array([1, 1, 1, 1])
```

```python
x1 = la.lstsq(A, test1)
```

```python
orth = la.orth(A)
```

```python
r = np.ptp(A,axis=1)
```

```python
r
```

    array([4, 2, 5, 2])

