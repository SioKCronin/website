---
title: Binet's Formula
menu:
    ai_notes:
        parent: Math
---
This proof was shared with me by my friend Chuck Larrieu Casias, and I liked
it so much I wanted to write it up here.

Suppose we have two similar rectangles, $A$ and $B$. Let $A$ have sides $a$ and $b$,
and $B$ have corresponding sides $b$ and $a+b$. 

Then $\frac{b}{a} = \frac{a+b}{b}$. Also, $\frac{b}{a} = \frac{a}{b} + 1$. 

Call $\phi = \frac{b}{a}$. Then $\phi = \frac{1}{\phi} + 1$.

Multiply both sides by $\phi$ to get $\phi^2 = \phi + 1$. Move all terms to one side
to get $\phi^2 - \phi - 1 = 0$. If you solve this quadratic for $\phi$ you get
$\phi = \frac{1 \pm \sqrt{5}}{2}$.

Call $\phi = \frac{1 + \sqrt{5}}{2}$, and $\psi = \frac{1 + \sqrt{5}}{2}$.

Notice:

$\phi^2 = \phi^1 + \phi^0$ 

$\phi^3 = \phi^2 + \phi^1$

$\phi^4 = \phi^3 + \phi^2$

$\phi^n = \phi^{n-1} + \phi^{n-2}$

Notice any sequence $U\_{n} = x\phi^n + y\psi^n$ also has fibonnaci relation:

$U\_{n} = x\phi^n + y\psi^n = x (\phi^{n-1} + \phi^{n-2}) + y ( \psi^{n-1} + \psi^{n-2})$

$= (x\phi^{n-1} + y \psi^{n-1}) + (x\phi^{n-2} + y \psi^{n-2})$ 

$= U\_{n-1} + U\_{n-2}$ 

Set $U\_{0} = 0$ and $U\_{1} = 1$ to get ${U\_{n} = 0, 1, 2, 3, 4, ...}$:q

Solve for $x$ and $y$. 

$U\_{0} = 0 = x \phi^{0} + y \psi^{0} = **x==-y**$

$U\_{1} = 1 = x \phi^{1} + y \psi^{1}$

$= -y\phi + y\psi$

$= y(\psi + \phi)$

**$y = \frac{1}{\psi - \phi}$**

$x = \frac{1}{\phi - \psi}$

So $U\_{n} = \frac{1}{\phi-\psi}\phi^{n} + \frac{1}{\psi-\phi}\psi^n$

Algebra tap dance here.

$= \frac{(1-\sqrt{5})^2 - (1-\sqrt{5})^n}{2^n\sqrt{5}}$
