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


$$ \begin{align} \nabla_{\theta} E_x[f(x)] &= \nabla_{\theta} \sum_x p(x) f(x) & \text{definition of expectation} \ & = \sum_x \nabla_{\theta} p(x) f(x) & \text{swap sum and gradient} \ & = \sum_x p(x) \frac{\nabla_{\theta} p(x)}{p(x)} f(x) & \text{both multiply and divide by } p(x) \ & = \sum_x p(x) \nabla_{\theta} \log p(x) f(x) & \text{use the fact that } \nabla_{\theta} \log(z) = \frac{1}{z} \nabla_{\theta} z \ & = E_x[f(x) \nabla_{\theta} \log p(x) ] & \text{definition of expectation} \end{align} $$
