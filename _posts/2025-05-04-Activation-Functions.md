---
title: "Understanding Activation Functions in Deep Learning"
date: 2025-05-04 00:00:00 +0000
categories: [deep-learning]
tags: [activation-functions, relu, sigmoid, tanh, elu, maxout]
---
<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

# Activation Functions in Deep Learning

Activation functions are a critical part of deep neural networks. They introduce non-linearity, allowing neural networks to learn complex patterns in data.

---
## 1. Sigmoid

**Function:**

$$
\sigma(x) = \frac{1}{1 + e^{-x}}
$$

**Properties:**

- **Output Range**: $[0, 1]$
- **Used historically**: Common in early neural networks. 

**Problems:**

1. **Saturation**: For large positive or negative inputs, saturated neurons kills the gradients. This is because for those regions the slope tends to be zero. 
2. **Not Zero-Centered**: Can lead to inefficient gradient updates. This is because the all the weights tend to be in the same direction and the adjustments to reach the minimum takes more time.
3. **Exponential Cost**: Computing `exp()` can be expensive in large models.

---

## 2. Tanh

**Function:**

$$
\tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}}
$$

- **Range**: $[-1, 1]$
- **Zero-Centered**: More desirable than sigmoid for hidden layer activations.
- **Still Saturates**: Can suffer from vanishing gradients for extreme values.

---

