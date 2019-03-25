---
layout: blog
title: Machine Learning Note Week 3
date: 2019年3月12日17:18:26
tags: MachineLearning
categories: SJTU
---
# Classification 
To attempt classification, one method is to use linear regression and map all predictions greater than 0.5 as a 1 and all less than 0.5 as a 0. However, this method doesn't work well because classification is not actually a linear function.

The classification problem is just like the regression problem, except that the values we now want to predict take on only a small number of discrete values. For now, we will focus on the **binary classification problem** in which y can take on only two values, 0 and 1. (Most of what we say here will also generalize to the multiple-class case.) 
<!--more-->
For instance, if we are trying to build a spam classifier for email, then $x^{(i)}$may be some features of a piece of email, and y may be 1 if it is a piece of spam mail, and 0 otherwise. Hence, y∈{0,1}. 0 is also called the **negative class**, and 1 the **positive class**, and they are sometimes also denoted by the symbols “-” and “+.” Given $x^{(i)}$, the corresponding $y^{(i)}$ is also called the **label** for the training example. 

# Simplified Cost Function and Gradient Descent 
We can fully write out our entire cost function as follows:

$J(\theta)=-\frac{1}{m} \sum\_{i=1}^{m}\left[y^{(i)} \log \left(h\_{\theta}\left(x^{(i)}\right)\right)+\left(1-y^{(i)}\right) \log \left(1-h\_{\theta}\left(x^{(i)}\right)\right)\right]$

$\theta\_{j} :=\theta\_{j}-\frac{\alpha}{m} \sum\_{i=1}^{m}\left(h\_{\theta}\left(x^{(i)}\right)-y^{(i)}\right) x\_{j}^{(i)}$

A **vectorized** implementation is:

$\theta :=\theta-\frac{\alpha}{m} X^{T}(g(X \theta)-\vec{y})$