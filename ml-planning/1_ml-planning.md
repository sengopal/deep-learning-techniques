### Pick a single number evaluation
1. Picking F1 score
2. Picking average of error across different geographies

o what I found for a lot of machine learning teams is that having a well-defined dev set, which is how you're measuring precision and recall, plus a single number evaluation metric, sometimes I'll call it single row number.
Play video starting at :5:4 and follow transcript5:04
Evaluation metric allows you to quickly tell if classifier A or classifier B is better, and therefore having a dev set plus single number evaluation metric distance to speed up iterating.

But by tracking four numbers, it's very difficult to look at these numbers and quickly decide if algorithm A or algorithm B is superior. And if you're testing a lot of different classifiers, then it's just difficult to look at all these numbers and quickly pick one. So what I recommend in this example is, in addition to tracking your performance in the four different geographies, to also compute the average. And assuming that average performance is a reasonable single real number evaluation metric, by computing the average, you can quickly tell that it looks like algorithm C has a lowest average error. And you might then go ahead with that one. If you have to pick an algorithm to keep on iterating from. So your work load machine learning is often, you have an idea, you implement it and try it out, and you want to know whether your idea helped. So what we've seen in this video is that having a single number evaluation metric can really improve your efficiency or the efficiency of your team in making those decisions

### Satisficing and Optimizing Metric
1. Accuracy vs Runtime combination - 
   2. cost = acc - 05* running_time
3. So here's something else you could do instead which is that you might want to choose a classifier that maximizes accuracy but subject to that the running time, that is the time it takes to classify an image, that that has to be less than or equal to 100 milliseconds. So in this case we would say that accuracy is an **optimizing metric** because you want to maximize accuracy. You want to do as well as possible on accuracy but that running time is what we call a **satisficing metric.** 

> If you have N metrics that you care about it's sometimes reasonable to pick one of them to be optimizing. So you want to do as well as is possible on that one. And then N minus 1 to be satisficing, meaning that so long as they reach some threshold such as running times faster than 100 milliseconds, but so long as they reach some threshold, you don't care how much better it is in that threshold, but they have to reach that threshold. 

For "wake words" - you have at most one false positive every 24 hours of operation, right? So that your device randomly wakes up only once per day on average when no one is actually talking to it. So in this case accuracy is the optimizing metric and a number of false positives every 24 hours is the satisficing metric where you'd be satisfied so long as there is at most one false positive every 24 hours. 

### Train/Dev/Test Distributions
 make your dev and test sets come from the same distribution

Randomly shuffle all the data -> then identify dev and test sets


