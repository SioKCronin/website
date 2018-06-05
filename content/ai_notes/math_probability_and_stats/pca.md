---
title: Principal Component Analysis
menu:
    ai_notes:
        parent: Math, Probability & Stats
---

### Cool Result

Considering the decompostions $A = Q^{T}DQ$, where $Q$ is an orthogonal matrix and $D$ 
is the diagonal matrix of eigenvalues, the columns of $Q$ are the principal
components of our matrix! 

### How does it work?

Remember, $Y = XP$, where $P$ is the change of basis matrix. 

First we start with the covariance matrix $S\_{x} = \frac{1}{m}X^{T}X$,
where X is our input matrix. If every feature was necessary, with no redundancy, 
we'd see a diagonal covariance matrix where the only non-zero values would be 
lined up on the diagonal. But in many cases we'll need to sift through some
interactions to see what features stand out as principal components. 

Can we find a matrix that can transform our covariance matrix to a 
principal component basis?

Let's start by defining our target matrix as $S\_{y}$; a diagonal 
matrix where $S\_{y} = \frac{1}{m}Y^TY = \frac{1}{m}(XP)^T(XP) = \frac{1}{m}P^{T}X^{T}XP = P^TS\_{x}P$ (since we can substite Y = XP), 
and select $Q$ (the orthogonal matrix) as our $P$. This yields $S\_{y} = Q^TS\_{x}Q = Q^T(QDQ^T)Q = D$, 
which is what we wanted to find, since we know $D$ is a diagonal matrix of singluar values, 
the columns of which are the principal components of our input matrix. Furtheremore,
we have shown that this matrix $D$ is our new covariance matrix $S\_{y}$
where all products of feature pairs are zero except the products of the features with themselves,
which means we have reduced redundancy of signal to zero!

But hey, where did that orthogonal matrix $Q$ come from? One approach for 
determining $Q$ and $D$ from our original matrix is Singular Value Decomposition (SVD).
Remember, **singular values** are non-negative, real numbers that are the square root
of the eigenvalues of the self-adjoint operator $T\*$ ($T\*T: X \rightarrow X$), 
that is mapping from $X$ to itself. The word adjoint in this case is used to 
generalize the conjugate transpose to infinite-dimensional situations.

Here is an outline of the core equation of the decomposition.  

* $A\_{m \times n} = U\_{m \times m} * \Sigma\_{m \times n} * V^T\_{n \times n}$
* $U\_{m \times m}$: The columns of $U$ are **left singular vectors** of $A$ (the set of 
orthonormal eigenvectors of $AA^T$
* $\Sigma\_{m \times n}$: non-square diagonal matrix, where the entries are non-negative
real numbers (the singular values)
* $V^T\_{n \times n}$: The columns of $V$ are **right singular vectors** of $A$ (the set of 
orthonormal eigenvectors of $A^TA$. 
