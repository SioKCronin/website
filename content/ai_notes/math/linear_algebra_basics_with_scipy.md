---
title: Basics with Scipy
date: 2018-05-03
menu:
    ai_notes:
        parent: Math
---

```python
import scipy.linalg as la
import numpy as np
```

## Motivating example

We are entering three pies into the bakeoff, and want to make sure we win. We've tried a lot of different ingredients, but ultimatley have found that taste comes down to **butter**, **salt**, **sugar**, and **grandma's secret spice blend**. 


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


```python

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


