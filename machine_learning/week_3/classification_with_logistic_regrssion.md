# Classification With Logistic Regression

**Binary classification** - when there is only 2 classes (0/false or 1/true)

Linear regression is not a good method due to the small output range (0,1) and when there is a data point way outside the group will drastically change the outcome

- shift the decision boundary by a lot leading to misclassification

## Logistic Regression

**_Fits an S shape curve that stays within the boundaries 0 and 1_**

Steps for logistic regression:

1. Find $f_w,_b(x) = z = w * x + b$ where $*$ is the dot product
2. Take $z$ and put it into the sigmoid function $$g(z) = 1/(1+e ^{-z})$$

Logistic regression gives the probability the output will be 0 or 1

- $g(z) = 0.7$ means a 70% the input is positive

## Decision Boundary

**_The line that determines if the logistic regression predicts 0 or 1_**

It does not need to be a straight line

The decision boundary of $z$ will be when it becomes 0

- the equation solved after $z = 0$ is the equation for the decision boundary
