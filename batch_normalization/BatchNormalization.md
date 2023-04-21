## Batch Normalization

Mostly Z_2 is normalized, though a_2 can be normalized as well. Z is the input to the activation function a()

Compute mean and variance of zs in a single layer and normalize each value - mean zero and variance 1. 

But not all layers should have the same distribution, otherwise it is not learning - So a set of learnable parameters for each layer - gamma and beta are parameters are used --> which is learnt using SGD, or something similar and values are updated.

If gamma = variance and beta = mean, then it inverts normalization perfectly


> use pytorch and see how the beta and gamma for this layer changes

Note: Use of Batch normalization removes the usage of the bias term for the layer. Since it is added to all hidden units, it gets removed in the mean.  Instead beta_l of the Batch norm performs the bias parameter role. (n x 1) is the dimension of bias term and also for beta and gamma for batch norm as well.

Keeps and mean and variance same for the layer, irrespective of the weight changes - helps with numerical stability.

Slight Regularization effect: as mean and variance are calculated only for mini-batches instead of the entire training dataset, it introduces some bit of noise similar to dropout and helps in regularization. - But only slight

Test time: There are no mini batches at inference time and typically there is only one input variable. The batch norm keeps track of an "expontentially weighted average" of the mean and variances values of that particular layer using all of its previous mean and variances values (expontentially weighted average over previous values) and uses that during inference time to calculate z_norm and then recreate ~z using beta and gamma












