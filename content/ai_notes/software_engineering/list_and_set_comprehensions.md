---
title: List and Set Comprehensions
menu:
    ai_notes:
        parent: Software Engineering
draft: True
---

These are some of my favorite tools in Python, mostly because they read like poetry
and are super helpful in creating lists and sets.

'''python
>>> a = {x for x in "acatatetheshoe' if x not in 'cat'}
>>> a
{'e', 'h', 's', 'o'}
'''
