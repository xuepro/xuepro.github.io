---
layout:       post
title:        "Dynamic Programming"
subtitle:     "Dynamic Programming"
date:         2018-06-02 11:14:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - AI
    
---

##  Dynamic Programming

###  Policy Evaluation (Prediction)
For a given policy $$\pi$$ compute the state–value
function $$V^{\pi}$$

$$\begin{equation}\begin{split}
V^{\pi}(s) = E_{\pi}[r_{t+1}+ \gamma V^{\pi}(s_{t+1}) \vert s_t=s]\\ 
=\sum_{a\in A} \pi (a\vert s)(R(s,a)+\gamma \sum_{s' \in S}P(s' \vert s,a) V^{\pi}(s'))
\end{split}\end{equation} $$

A system of jSj simultaneous linear equations
Solution in matrix notation (complexity $$O(n^3))$$:

$$V^{\pi} = (1- \gamma P^{\pi})^{-1} R^{\pi}$$

### Iterative Policy Evaluation

Iterative application of Bellman expectation backup

V_0\rightarrow V_1\rightarrow V_2\rightarrow ...\rightarrow V_k\rightarrow ...\rightarrow V^{pi}

**A full policy–evaluation backup:**

$$V^{k+1}(s) =\sum_{a\in A} \pi (a\vert s)(R(s,a)+\gamma \sum_{s' \in S}P(s' \vert s,a) V^{k}(s'))


A **sweep** consists of applying a backup operation to each state
Using **synchronous** backups
 - At each iteration k + 1
 - For all states $$s\in S$$
 - Update $$V^{k+1}(s)$$ from $$V^{k}(s\prime)$$
 
 
