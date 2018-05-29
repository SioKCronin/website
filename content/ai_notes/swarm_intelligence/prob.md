
# Prob

\begin{align}
\dot{x} & = \sigma(y-x) \\\\\\
\dot{y} & = \rho x - y - xz \\\\\\
\dot{z} & = -\beta z + xy
\end{align}

$$\alpha = 1000$$


```python
import matplotlib
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
```

    /usr/local/lib/python3.6/site-packages/matplotlib/font_manager.py:278: UserWarning: Matplotlib is building the font cache using fc-list. This may take a moment.
      'Matplotlib is building the font cache using fc-list. '



```python
x = np.linspace(0, 3*np.pi, 500)
plt.plot(x, np.sin(x**2))
plt.title('A simple chirp')
plt.show()
```


![png](prob_4_0.png)



```python

```
