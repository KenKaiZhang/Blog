# Gradient Descent in Practice

**_Multiple features risks the possibilities of certain features overshadowing other features due to how big the values can be._**

- number of bedrooms will be immensily smaller than the square footage of a house

Possible solution is to adjust the weights so they become a multiplier that can help even the features out

- $w_1$ = 0.1 and a $w_2$ of 50 can help features where $x_1$ = 100000 and $x_2$ = 5

That solution is not the best since it results in a gradient descent that would take too long to the minima since a small adjustment to one parameter can throw the algorithm off

**Solution**: scale data before training so features in a similar range

## Scaling Features

Common methods:

- divide by the maximum
- mean normalization
- z-score normalization

_Note:_ Aim to get around $-1 ≤ x_j ≤ 1$ for each feature $x_j$

## Building a Good Gradient Descent

A good method to check if the algorithm is working is by plotting the iteration x $J(w,b)$ relation where each point in the graph indicates the cost of a $w$ and $b$ at a specific iteration

- helps see if cost is headed towards 0
- helps see at what iteration there is no need for more (when the curve flattens)

If the cost is going up and down or continuously increasing, then there could be a bug or the learning rate is too large

A way to test if its a bug and not alpha is to choose an extremely small alpha and see if there is a behavioural change

- small alpha is a debugging step not a reccomendation

Common alpha values:

- 0.0001
- 0.001
- 0.01
- 1

**Feature engineering** - using intuition to design new features by transforming or combining given ones
