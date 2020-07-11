---
title: Decorators and Metaclasses
menu:
    ai_notes:
         parent: Software Engineering
---

Let's explore each in turn, and then explore when each might be most useful.

### Counter

Counter is a dictionary subclass with no restrictions on keys and
values.

```python
from collections import Counter
words = ['apples','oranges', 'apples', 'apples']
words1 = ['oranges', 'oranges', 'oranges', 'apples']
```
```python
# Return (element, count) pairs for n most common
Counter(words).most_common()
```
```python
# Subtract elements from another mapping
w = Counter(words)
w1 = Counter(words1)
w.subract(w1) # subtraction, includes zero and negatives
w - w1 # subtraction, only positive counts
w & w1 # intersection
w | w1 # union
w + w1 # adds two counters together
```
```python
# Some useful patterns
c.clear() # reset all counts
dict(c) # convert to a dictionary
c.items() # convert to a list of (element, count) pairs
Counter(dict(list_of_pairs)) # convert from a list of (element, count)
pairs
c.most_common()[:-n-1:-1] # n least common elements
c += Counter() # remove zero and negative counts
```

### deque
Deques are generalizations of stacks and queues that supports appends and pops
from either side of the deque. 

```python
d = deque('hi')
append('gh') # append 'gh' to the right of the deque
appendleft('t') # append 't' to the left of the deque
rotate(1) # right rotation, everything shifts 1 to the right
rotate(-1) # left rotation, everythign shifts 1 to the left
d.pop() # remove the rightmost item, 'h'
d.popleft() # remove the leftmost item, 't'
new = deque(reversed(d)) # make a new deque in reverse order
d.extendleft('abc') # reverses the input order, similar to append('cba')
```
```python
# Here's a fun example from the Python docs showing how to slice an index
def delete_nth(d, n):
    d.rotate(-n)
    d.popleft()
    d.rotate(n)
```

### defaultdict

Returns a dictionary-like object.

```python
s = 'useful'
d = defaultdict(int)
for k in s:
    d[k] += 1

>>>d.items()
[('u', 2), ('s', 1), ('e', 1), ('f', 1), ('l', 1)]
```

### namedtuple()

The fields of the tuple are referenceable by name

```python
>>>score = namedtuple('score', ['stephen', 'pearl'])
>>>s = score(10, pearl=10)
>>>p.stephen
10

>>>s = score('stephen'=10, 'pearl'=10)
>>>s._asdict()
OrderedDict([('stephen', 10), ('pearl', 10)])

>>>s._fields
('stephen', 'pearl')

# Convert dicts to namedtuple
>>>d = {'stephen':10, 'pearl':10}
>>>score(**d)
score(stephen=10, pearl=10)
```

### OrderedDict

OrderedDicts are dictionaries that remember the order items were
inserted (items are returned in the order their keys were added). 

```python
>>> d = {'stephen': 1,'pearl': 2, 'lion': 3}

# Sort value by key
>>> OrderedDict(sorted(d.items(), key=lambda t: t[0]))
OrderedDict([('lion', 3), ('pearl', 2), ('stephen', 1)])

# Sort value by value
>>> OrderedDict(sorted(d.items(), key=lambda t: t[1]))
OrderedDict([('stephen', 1), ('pearl', 2), ('lion', 3)}
```

Since Python 3.2 you can move specific keys to the head or tail, using the **move_to_end** method.
