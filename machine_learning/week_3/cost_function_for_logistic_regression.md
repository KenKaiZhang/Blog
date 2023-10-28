# Cost Function for Logistic Regression

The **squared error loss function** used by linear regression is not a good choice since it results in a non-convex cost graph that has multiple local minimas that gradient descent will encounter

We uses a **logistic loss function**:

$$L(f_{w,b}(x^i), y^i) = -log(f_{w,b}(x^i))$$
$$L(f_{w,b}(x^i), y^i) = -log(1 - f_{w,b}(x^i))$$

where the the top one is when $y^i = 1$ and the bottom is $y^i = 0$

Why?

1. The top one only works when $y = 1$ because when you look at a log functin between 0 and 1 (since that's the only range we carea about), the graph will start high y-axis and end closer to y-axis 0 as x approaches 1
2. The bottom one only works for $y = 0$ because the log function will start at (0,0) and head towards y-axis infinity as you approach 1 indicating that the prediction is straying farther from the expected value (0)

## Simplified

$$L(f_{w,b}(x^i), y^i) = - y^ilog(f_{w,b}(x^i)) - (1 - y^i)log(1 - f_{w,b}(x^i))$$

The equation is the same as the divided one presented above because when $y$ is 1 or 0, one of them gets canceled out resulting in just one of the terms remaining

## Cost function

$$J(w,b) = 1/m\sum[L(f_{w,b}(x^i), y^i) ]$$

Derived from the maximum likelihood idea from statistcs
