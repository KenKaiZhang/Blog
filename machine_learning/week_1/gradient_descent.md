# Gradient Descent

**_The systematic way to find the smallest value of any function_**

1. Have some function $J(w,b)$
   - can be any function
2. Start with some $w$ and $b$
3. Keep changing $w$ and $b$ to reduce $J(w,b)$ to reach as close to the minimum as possible

_It is possible to have multiple minimums (**local minima**)_

## Implementing

$$w = w - a [(d/dw) J(w,b)]$$
$$b = b - a[(d/db) J(w,b)]$$

- $w$ and $b$ is getting reassigned
- $a$ is the learning rate
  - small positive number that controls the step size
  - bigger == more aggressive downhill descent
- $(d/dw) J(w,b)$ and $[(d/db) J(w,b)]$ is the partial derivative of the cost function with respect to the weights

Repeat until convergence and update $w$ and $b$ at the same time

## Intuition

_Since I cannot put images, imagine the following_

Imagine the cost function $J(w)$ that is in the shape of a U

- should be since thats what a single variable cost function looks like

If the current cost function results in a cost on the right side of the U, then we will have a positive slope

- the derivative of $J(w)$ is the slope of the line tangent to point $w$ in the cost function $J(w)$

Since the slope is positive, if we plug it into the equation $w = w - a (positive)$, we should get a negative $a$ causing $w$ to move to the left of the U, which is correct since $w$ is being shifted towards the bottom from being to positive

- this statement is true if $w$ was on the left side of the U

## Learning Rate

If $a$

- is too small can lead to many calculations and a very slow process
- is too large can miss the minimum and fail to converge and begin to diverge

Local minimum can be hit with a fixed learning rate because

1. if the weight is at the local minimum, then the slope would be 0 and weight will fail to update
2. if the weight is moving towards the local minimum, it will naturally slow down due to the shape of the weight x cost function graph (the slope will naturally level)

## Gradient Descent for Linear Regression

By plugging in the linear formula $wx + b$ for $f_w,_b(x)$ in $J(w,b)$, the gradient descent formulas can be shortened to

$$d/dwJ(w,b) = 1/m \sum(f_w,_b(x^i) - y^i)x^i$$

$$d/dbJ(w,b) = 1/m \sum(f_w,_b(x^i) - y^i)$$

**Convex function** will always have one GLOBAL minimum
