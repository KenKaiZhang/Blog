# Regression Model

**_Models used to predict numbers_**

**Linear regression** - using data to create a line of best fit and using that to calculate the output of a given input

**Notation:**

- **x**: the input or feature
- **y**: the output or target
- **m**: the number of training examples
  - `(x,y)` indicates a single training example

Training a model involves taking a **training set**, feeding it to a learning algorithm to get a function **_f (or model)_**

**y-hat** is the prediction while **y** is the truth

**Univariate linear regression:** $ f_w,\_b(x) = wx + b $

- basically finding the best slope function where $b$ is the y-intercept and $w$ represents the slope of the line
- $f(x)$ is basically y-hat

## Cost Function

**_A function used to mesure how accurate a model is by calculating the average of the error_**

$w$ and $b$ are the adjustable **parameters** or **coefficients** or **weights** that determines how accurate the model will be after training

**Common linear regression cost function (squared error cost function):**

$$J(w,b) = 1/2m ∑(yhat - y)^2$$

- $yhat - y$ indicates the **error**
- we want the error of the ENTIRE training set ($m$)
- to avoid the cost function from continuously getting bigger as $m$ gets bigger, we multiply the sum by $1/2m$
  - the average square error
  - $2m$ is to make the calculation neater and just common practice

**We want to minimize $J(w,b)$**
