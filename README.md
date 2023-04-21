# Model Training Playbook and Experiments




https://www.linkedin.com/posts/victor-sanh_multimodal-llm-deeplearning-activity-7038583909994885120-BjsF/?utm_source=share&utm_medium=member_android

https://docs.google.com/document/d/1ZNGyVWYFUbzV0xuei4SED2QAakGjMpaaQALcKYQm46U/edit#heading=h.66l93vag25o8

Deep learning Tuning playbook

Papers in Zotero

Write a review paper - using these techniques and its demonstration on few toy datasets


### Techniques to explore
A few other architecture changes we ablated and that turned out to be beneficial
Ditch the biases in all `nn.Linear`
Slack context
Standard LayerNorm -> RMSNorm
Slack context


### Hyperparameters (order of importance)
1. learning_rate 
2. momentum - beta (~0.9),number of hidden units and mini batch size
3. number of layers and learning_rate_decay
4. Not usually tuned - adam - beta1(0.9), beta2(0.999), epsilon (10**-8)

Try random values: do not use a grid - this allows you to test a more set of values for more important ones
Also find a good set of values, then focus on that area in that area density

Rather than sampling at random, choose a range for random values

Appropriate scale for searching uniformly in log scale for learning_rate from 0.0001 to 0.1 or 1, instead of uniform across all values
for sampling across logarthmic scale
r = -4 * np.random.rand()
alpha = 10**r 

beta - exponentially weighted averages
temperature - 0.9 means averaging over last 10 values and 0.999 means averaging over 10000 values
(1-beta) is the value to be sampled.
(1 - beta) = 0.1 to 0.001
goal: sample as many values between 0.9 to 0.99 similar to number of values between 0.99 to 0.999

r = [-3, -1] 
1 - beta = 10**r
beta = 1 - 10**r

Note: values between 0.9000 to 0.9005 for averaging is around 10, but for 0.999 (last 1000 values) to 0.9995 (last 2000 values), 1 - beta is very sensitive to small changes as it gets closer to 1. So using (1 - beta) allows to sample better.

Co-variate shift (ground truth function shifts)


