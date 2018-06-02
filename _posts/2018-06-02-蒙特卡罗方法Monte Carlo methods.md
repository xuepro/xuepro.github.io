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

$$ \pi(s) = \leftarrow arg\max_{a\in A} p(s^{\prime} ,r \vert s,a) [r+ \gamma V(s^{\prime} )] $$

Without a model, however, state values alone are not sufficient. One must explicitly
estimate the value of each action in order for the values to be useful in suggesting a policy.
Thus, one of our primary goals for Monte Carlo methods is to estimate $$Q^*(s,a)$$.

### Monte Carlo Prediction (Estimation of State Values)

#### First–Visit Monte–Carlo Policy Evaluation
  
**Initialize:**
$$\pi \leftarrow $$   policy to be evaluated
$$V \leftarrow $$  an arbitrary state–value function
Returns(s)  $$\leftarrow $$  an empty list, for all $$\forall s \in S$$

**loop**

Generate an episode using $$\pi$$

**for** each state s in the episode **do**

  - $$R \leftarrow $$  return following the first occurrence of s
  
  - Append $$R$$ to Returns(s)
  
  - $$V(s)\leftarrow $$   average(Returns(s))
  
  
**end for**

**end loop**




### Monte Carlo Estimation of Action Values
