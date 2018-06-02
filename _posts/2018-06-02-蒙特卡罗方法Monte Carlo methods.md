---
layout:       post
title:        "蒙特卡罗方法Monte Carlo methods"
subtitle:     "Monte Carlo methodsg"
date:         2018-06-02 17:47:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - AI
    
---

Previously, we discussed markov decision processes, and algorithms to find the optimal action-value function 
$$q^*(s,a)$$ and $$v^*(s)$$. We used **policy iteration** and **value iteration** to solve for the optimal policy.

But it comes with many restrictions. For example, are there a lot of real world problems where you know the state transition probabilities?  Can you arbitrarily start at any state at the beginning? Is your MDP finite?

Monte Carlo methods look at the problem in a completely novel way compared to dynamic programming. It asks the question: *How many samples do I need to take from our environment to discern a good policy from a bad policy?*

With a model, state values alone are sufficient to determine a policy; one simply looks ahead one step and chooses whichever
action leads to the best combination of reward and next state, as we did in the chapter on DP.

$$ \pi(s) = \leftarrow arg\max_{a\in A} p(s^{\prime} ,r \vert s,a) [r+ \gamma V(s^{\prime} ) $$
