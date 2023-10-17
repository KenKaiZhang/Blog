# Multiple Features

Previous model linear regression: $f_w,_b(x) = wx + b$

New model with consideration for multiple features (**_multiple linear regression_**):

$$f_w,_b(x) = w_1x_1 + w_2x_2 + ... + w_jx_j + b$$

- $j$ is the feature
- $b$ is the base case

The weights and the features are now notated as **_vectors_** so the new formula can be shortened to $f_w,_b(x) = w * x + b$ where $w * x$ is the dot product between the two vectors

## Vectorization

Can help simplify code from

```python
f = 0
for j in range(n):
    f = f + w[j] * x[j]
f = f + b
```

to

```python
f = np.do(w,x) + b
```

where

```python
x = np.array([10,20,30])
w = np.array([1.0, 2.5, -3.3])
b = 4
```

Also makes the code run faster since Numpy has the ability to compute via parallel hardware

## Gradient Descent for Multiple Linear Regression

**Model**: $f_w,_b(x) = w_1x_1 + w_2x_2 + ... + w_jx_j + b$

**Cost Function**: $J(w_1, ..., w_n, b)$

**Gradient Descent**:

1. $w_1 = w_1 - \alpha (1/m)\sum (f_w,_b(x^i) - y^i)x_1^i$
2. $w_2 = w_2 - \alpha (1/m)\sum (f_w,_b(x^i) - y^i)x_2^i$
3. $w_3 = w_3 - \alpha (1/m)\sum (f_w,_b(x^i) - y^i)x_3^i$

up to $w_n = w_n - \alpha (1/m)\sum (f_w,_b(x^i) - y^i)x_n^i$

- $b = b - \alpha (1/m)\sum (f_w,_b(x^i) - y^i)$

_Note_: A **normal equation** is a method unqiue to linear regression that can solve for $w$ and $b$ without iteration
