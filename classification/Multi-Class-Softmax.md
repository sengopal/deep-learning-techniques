## Softmax function
performs e**z of the values that are from the final layer and then normalized by their mean to computer probabilities that sum to 1.

Loss = log-loss = - sum(y * log y_hat) 

Example: -y_2 * log Y_hat2 ( for C=2 for the correct one)
y_hat2 needs to be large for loss to be minimal.

Y = 4xm => for 4 classes and m examples

