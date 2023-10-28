# The Problem of Overfitting

**_When the model fails to follow the trend of the data_**

Two types of fitment issues:

- **underfitting (high bias)**: the model is not fitting the training data
- **overfitting (high variance)**: the model is fitting the data way too well and will not generalize

## Addressing Overfitting

There are 3 main ways to address overfitting

Collect more data

**Feature selection**: choosing features to include/exclude

- could result in good features being unconsidered

**Regularization**: reducing the impact of certain features by reducing their weights

- allows you to keep all your features
- usually only change $w_j$

## Cost Function with Regularization

We can reduce the effect of the features through weights by penalizing them in the cost function

$J(w,b) + 1000w_3^2 + 1000w_4^2$

If we want all features $w_1 ... w_n$, we can penalize all of them througha **regularization parameter**

$$J(w,b) = 1/2m \sum (f_{w,b}(x^i) - y^i)^2 + \lambda/2m \sum w_j^2$$

The formula allows for the regularization to work even as the data set increases over time

- forces algorithm to fit the data while keeping $w_j$ small
- really small $\lambda$ will overfit while a really big $\lambda$ will underfit

## Regularized Linear Regression and Logistic Regression

The gradient descent for linear regression

$$w_j = w_j - \alpha (dJ/dw)[1/m \sum[(f_{w,b}(x^i) - y^i)x_j^i] + (\lambda/m)w_j]$$
$$b = b -\alpha (dJ/db) 1/m \sum (f_{w,b}(x^i) - y^i) $$

We don't include the lambda for $b$ since we don't regularize it

Logistic regression is basically the same thing but you replace the cost function in the algorithm with the one used for logistic regression
