### end to end learning
Take speech recognition as an example, where your goal is to take an input X such an audio clip, and map it to an output Y, which is a transcript of the audio clip. 
what end-to-end deep learning does, is you can train a huge neural network to just input the audio clip, and have it directly output the transcript.


It's only when you have a very large data set, you know one could say 10,000 hours of data, anything going up to maybe 100,000 hours of data that the end-to end-approach then suddenly starts to work really well. So when you have a smaller data set, the more traditional pipeline approach actually works just as well. Often works even better. And you need a large data set before the end-to-end approach really shines. And if you have a medium amount of data, then there are also intermediate approaches where maybe you input audio and bypass the features and just learn to output the phonemes of the neural network, and then at some other stages as well. So this will be a step toward end-to-end learning, but not all the way there. 

But when there is lack of data, 2-step works better - for example, face recognition - image cropping and then face matching as two different steps

English translation - end to end possible - since there are lot of (english,french) text pairs.

Estimation of childs age from xray - to determine growth rate - 2 steps - determine bones length and predict age from a lookup table.

### Pros and cons
1. allows data to speak, rather than forced feature representations
2. simplified workflow

1. large amount of data
2. misses out on useful hand-designed components -  hand-designed components tend to help more when you're training on a small training set.

For example of an autonomous system
you want to use machine learning or use deep learning to learn some individual components and when applying supervised learning you should carefully choose what types of X to Y mappings you want to learn depending on what task you can get data for. And in contrast, it is exciting to talk about a pure end-to-end deep learning approach where you input an image and directly output a steering. But given data availability and the types of things we can learn with neural networks today, this is actually not the most promising approach or this is not an approach that I think teams have gotten to work best


