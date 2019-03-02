---
layout: blog
title: KMP Algorithm
date: 2018-11-30 13:44:39
tags: Algorithm
---
# Introduction && Core thoughts

Calculate the **maximum shifting digits** based on the **characterics** of the given patten string.

# How to calculate?

Suppose we have a pattern string `p[0:n]` and the comparation failure happened when comparing `s[i+j]` with `p[j]` (when comparing `s[i:i+n]` with `p[0:n]`), that indicates that `s[i:j-1]` are already known and are equal to `p[0:j-1]`. So that suggests us to take a great heap as much as possible provided that 

Notice that when the failure happens at `p[j]`, the digits before are already clearify and can tell whether the *naive comparsion* will succeed or not.

# Visualization

I think these two pictures can clearly illustrate the phenomenon:

![failurefunction](https://res.cloudinary.com/ainevsia/image/upload/v1550225359/FailureFunction.png)

![calculate](https://res.cloudinary.com/ainevsia/image/upload/v1550225360/Calculation.png)

# Acknowledgements
A lot of thanks to [KMP算法详解](https://blog.csdn.net/yutianzuijin/article/details/11954939) which let me understand this algorithm.
