# Gradient Descent for Logistic Regression

The concept is the same as linear regression, the only thing that has changed is what $f(x)$ is

Repeat:

$$w_j = w_j - \alpha [1/m \sum (f_{w,b}(x^i) - y^i)x_j^i]$$
$$b = b - \alpha [1/m \sum (f_{w,b}(x^i) - y^i)]$$

where $f_{w,b}(x)$ is now the logistic regression formula
