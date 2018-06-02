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

-----------------------------------------
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

![](https://wx4.sinaimg.cn/mw690/006Lkwkygy1frx058hr1vj30of0awwfi.jpg)

-----------------------------------------

### Monte Carlo Estimation of Action Values

The only complication is that many state{action pairs may never be visited. If $$\pi$$ is
a deterministic policy, then in following $$\pi$$ one will observe returns only for one of the
actions from each state. With no returns to average, the Monte Carlo estimates of the
other actions will not improve with experience. 

One way to do this is by specifying that the episodes start in a state-action pair, and that every pair has a nonzero probability of
being selected as the start. This guarantees that all state{action pairs will be visited an
innite number of times in the limit of an innite number of episodes. We call this the
assumption of **exploring starts**.


![](https://wx4.sinaimg.cn/mw690/006Lkwkygy1frx058hhwij30of0d675w.jpg)

### Monte Carlo Control without Exploring Starts

How can we avoid the unlikely assumption of exploring starts? The only general way to
ensure that all actions are selected infinitely often is for the agent to continue to select
them. There are two approaches to ensuring this, resulting in what we call *on-policy*
methods and *off-policy* methods. *On-policy* methods attempt to evaluate or improve the
policy that is used to make decisions, whereas *off-policy* methods evaluate or improve
a policy dierent from that used to generate the data.

In on-policy control methods the policy is generally soft, meaning that $$\pi(a\vert s)>0 $$
for all $$s in S$$ and all $$a \in A(s)$$, but gradually shifted closer and closer to a deterministic
optimal policy.

The on-policy method we present in this section uses *$$\epsilon$$-greedy* policies.

That is, all nongreedy actions are given the minimal probability of selection, $$\frac{\epsilon}{\vert A(s)\vert}$$ and the remaining bulk of the probability,  $$1-\epsilon+ \frac{\epsilon}{\vert A(s)\vert}$$ .
*$$\epsilon$$-greedy* policies are
examples of *$$\epsilon$$-soft* policies,

![](https://wx4.sinaimg.cn/mw690/006Lkwkygy1frx058kuk6j30oh0flabw.jpg)

### Incremental Implementation

![](https://wx1.sinaimg.cn/mw690/006Lkwkygy1frx058i4txj30oh0eadh7.jpg)

### Off-policy Monte Carlo Control

![](https://wx2.sinaimg.cn/mw690/006Lkwkygy1frx058jt9vj30oh0exq4g.jpg)
