---
layout:       post
title:        "策略梯度Policy Gradient"
subtitle:     "策略梯度Policy Gradient"
date:         2018-06-10 11:24:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - AI
    
---

## 策略梯度Policy Gradient

The general case is that when we have an expression of the form $$E_{x \sim p(x \mid \theta)} [f(x)] $$ - i.e. the expectation of some scalar valued score function $$f(x)$$ under some probability distribution $$p(x;\theta)$$ parameterized by some $$\theta$$. Hint hint, $$f(x)$$ will become our reward function (or advantage function more generally) and $$p(x)$$ will be our policy network, which is really a model for$$ p(a \mid I)$$, giving a distribution over actions for any image $$I$$. Then we are interested in finding how we should shift the distribution (through its parameters $$\theta$$ to increase the scores of its samples, as judged by $$f\$$ (i.e. how do we change the network's parameters so that action samples get higher rewards). We have that:



$$\begin{equation}  \begin{split} 
\nabla_{\theta} E_x[f(x)] &= \nabla_{\theta} \sum_x p(x) f(x) &  \text{definition of expectation} \\ 
& = \sum_x \nabla_{\theta} p(x) f(x) & \text{swap sum and gradient} \\ 
& = \sum_x p(x) \frac{\nabla_{\theta} p(x)}{p(x)} f(x) & \text{both multiply and divide by } p(x) \\
& = \sum_x p(x) \nabla_{\theta} \log p(x) f(x) & \text{use the fact that } \nabla_{\theta} \log(z) = \frac{1}{z} \nabla_{\theta} z \\
& = E_x[f(x) \nabla_{\theta} \log p(x) ] & \text{definition of expectation} 
\end{split}\end{equation} $$


