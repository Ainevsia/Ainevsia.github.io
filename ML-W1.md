---
layout: blog
title: Machine Learning Note
date: 2019年3月7日17:34:24
tags: MachineLearning
categories: SJTU
---
# What is Machine Learning?
Two definitions of Machine Learning are offered.
> Arthur Samuel described it as: "the field of study that gives computers the abilit3y to learn without being explicitly programmed." This is an older, informal definition.

> Tom Mitchell provides a more modern definition: "A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E."

<!--more-->

## Example: playing checkers.
E = the experience of playing many games of checkers  
T = the task of playing checkers.  
P = the probability that the program will win the next game.  
In general, any machine learning problem can be assigned to one of two broad classifications:
Supervised learning and Unsupervised learning.

# Machine Learning Algorithms
- Supervised Learning
- Unsupervised Learning

## Supervised Learning
In supervised learning, we are given a data set and already know what our correct output should look like, having the idea that there is a relationship between the input and the output.  
Supervised learning problems are categorized into "regression" and "classification" problems.
- In a regression problem, we are trying to predict results within a continuous output, meaning that we are trying to map input variables to some continuous function.
- In a classification problem, we are instead trying to predict results in a discrete output. In other words, we are trying to map input variables into discrete categories. 
> Example 1:  
Given data about the size of houses on the real estate market, try to predict their price. Price as a function of size is a continuous output, so this is a regression problem.  
We could turn this example into a classification problem by instead making our output about whether the house "sells for more or less than the asking price." Here we are classifying the houses based on price into two discrete categories.

> Example 2:  
(a) Regression - Given a picture of a person, we have to predict their age on the basis of the given picture  
(b) Classification - Given a patient with a tumor, we have to predict whether the tumor is malignant or benign. 

## Unsupervised Learning
Unsupervised learning allows us to approach problems with **little or no idea** what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.  
We can derive this structure by clustering the data based on relationships among the variables in the data.  
With unsupervised learning there is no feedback based on the prediction results.
> Example:  
Clustering: Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.  
Non-clustering: The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. (i.e. identifying individual voices and music from a mesh of sounds at a cocktail party).

# Linear Regression

## Model Representation

To establish notation for future use, we’ll use $x^{(i)}$ to denote the “input” variables (living area in this example), also called input features, and $y^{(i)}$ to denote the “output” or target variable that we are trying to predict (price). A pair $\left(x^{(i)}, y^{(i)}\right)$ is called a training example, and the dataset that we’ll be using to learn—a list of m training examples $\left(x^{(i)}, y^{(i)}\right); i=1,...,m$
—is called a training set. 

Note that the superscript “(i)” in the notation is simply an index into the training set, and has nothing to do with exponentiation. We will also use X to denote the space of input values, and Y to denote the space of output values. In this example, X = Y = ℝ. 

To describe the supervised learning problem slightly more formally, our goal is, given a training set, to learn a function h : X → Y so that h(x) is a “good” predictor for the corresponding value of y. For historical reasons, this function h is called **a hypothesis**. Seen pictorially, the process is therefore like this:

![process](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/H6qTdZmYEeaagxL7xdFKxA_2f0f671110e8f7446bb2b5b2f75a8874_Screenshot-2016-10-23-20.14.58.png?expiry=1552089600000&hmac=OcPfeFN23lwgrmm7l_RkGIID6ssSzNbRCB5Fei6gvWM)

When the target variable that we’re trying to predict is continuous, such as in our housing example, we call the learning problem a regression problem. When y can take on only a small number of discrete values (such as if, given the living area, we wanted to predict if a dwelling is a house or an apartment, say), we call it a classification problem.

## Cost Function
We can measure the accuracy of our hypothesis function by using a cost function. This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

​$J\left(\theta\_{0}, \theta\_{1}\right)=\frac{1}{2 m} \sum\_{i=1}^{m}\limits\left(\hat{y}\_{i}-y\_{i}\right)^{2}=\frac{1}{2 m} \sum\_{i=1}^{m}\limits\left(h\_{\theta}\left(x\_{i}\right)-y\_{i}\right)^{2}$

> 注释：方差(Mean squared error)的1/2。统计学中参数估计部分的内容。

To break it apart, it is $\frac{1}{2}\bar{x}$ where $\bar{x}$ is the mean of the squares of $h\_{\theta}\left(x\_{i}\right)-y\_{i}$, or the difference between the predicted value and the actual value.

This function is otherwise called the "Squared error function", or **"Mean squared error"**. The mean is halved 
$\left(\frac{1}{2}\right)$ as a convenience for the computation of the gradient descent(梯度下降), as the derivative(导数) term of the square function will cancel out the $\frac{1}{2}$ term. The following image summarizes what the cost function does: 

![](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/R2YF5Lj3EeajLxLfjQiSjg_110c901f58043f995a35b31431935290_Screen-Shot-2016-12-02-at-5.23.31-PM.png?expiry=1552089600000&hmac=2dZ56IZcn2hSeASlmgGIKZlc-0y6clLNiFpj6lfInjE)

## Cost Function - Intuition I
If we try to think of it in visual terms, our training data set is scattered on the x-y plane. We are trying to make a straight line (defined by hθ(x)) which passes through these scattered data points.

Our objective is to get the best possible line. The best possible line will be such so that the average squared vertical distances of the scattered points from the line will be the least. Ideally, the line should pass through all the points of our training data set. In such a case, the value of J(θ0,θ1) will be 0. 

Thus as a goal, we should try to minimize the cost function. In this case, θ1=1 is our global minimum. 

## Cost Function - Intuition II
A contour plot(等高线地形图) is a graph that contains many contour lines. A contour line of a two variable function has a constant value at all points of the same line.