---
title: Covariance Shift
menu:
    ai_notes:
        parent: Math, Proability & Stats
draft: True
---

The question of covariance shift was first presented to me by Jason Hirshman at
Uncountable, who asked me how we might account for the fact that we were cross-validating
on training data that was, in all likelihood, distributed differently than our test data.
I had never considered that before, having always developed models where the training
and testing distributions were similar. I poked around for useful research paper,
and came across this, which I'd like to expand a bit here.
