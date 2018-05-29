---
title: itertools in Python
menu:
    ai_notes:
        parent: Software Engineering
---

There are lots of useful iteration tools in this module, and here are
some of my favorites. I thought
[this](http://jmduke.com/posts/a-gentle-introduction-to-itertools/) was a fun intro post for more
context.

### accumulate()

```python
>>> n_of_marbles = [1, 2, 3]
>>> list(accumulate(n_of_marbles, operator.add)
[1, 3, 6]
```

### count()

```python
>>> [i for i in count(1,1)]
[1, 2, 3, ...]

```

### cycle()

### repeat ()

### filterfalse()

### groupby()

### starmap()

### takewhile()

### permutations()

### combinations () and combinations_with_replacement()




