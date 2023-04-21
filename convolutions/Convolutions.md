
Convolution vs Cross-corelation
We are actually doing `Cross-corelation` but call it Convolution though the mirroring of the filters is skipped.
Kernels or filters are usually 3-dimensional

### Convolution
In a Conv network, the image size reduces as we go through layers, while number of channels/filters will increase.

### Max Pooling
hyperparameters for pooling are f, the filter size and s, the stride, and maybe common choices of parameters might be f equals two, s equals two. This is used quite often and this has the effect of roughly shrinking the height and width by a factor of above two,

 max pooling is used much more often than average pooling with one exception, which is sometimes very deep in a neural network. You might use average pooling to collapse your representation from say, 7 by 7 by 1,000. An average over all the spacial sense , you get 1 by 1 by 1,000. 
 
max pooling layers are 2-dimensional and applied repeatedly over all channels of the input.

max pooling - usually, it does not use any padding. So, the most common value of p by far is p equals zero.

### Layer Identification
And because the pooling layer has no weights, has no parameters, only a few hyper parameters, I'm going to use a convention that Conv 1 and Pool 1 shared together. I'm going to treat that as Layer 1, although sometimes you see people if you read articles online and read research papers, you hear about the conv layer and the pooling layer as if they are two separate layers. But this is maybe two slightly inconsistent notation terminologies, but when I count layers, I'm just going to count layers that have weights. So we treat both of these together as Layer 1. And the name Conv1 and Pool1 use here the 1 at the end also refers the fact that I view both of this is part of Layer 1 of the neural network

### Hyperparameters
Use standard literature first

### Activation and Parameters
notice that the max pooling layers don't have any parameters. Second, notice that the conv layers tend to have relatively few parameters, as we discussed in early videos. And in fact, a lot of the parameters tend to be in the fully collected layers of the neural network. And then you notice also that the activation size tends to maybe go down gradually as you go deeper in the neural network. If it drops too quickly, that's usually not great for performance as well. So it starts first there with 6,000 and 1,600, and then slowly falls into 84 until finally you have your Softmax output. You find that a lot of will have properties will have patterns similar to these


### Advantages of CNN
1. Parameter sharing - parameters are the filter values - a feature detector like a vertical edge detector computes it for the upper left-hand corner of the image. The same feature seems like it will probably be useful, has a good chance of being useful for the lower right-hand corner of the image. So, maybe you don't need to learn separate feature detectors for the upper left and the lower right-hand corners of the image.

2. Sparsity of connections - if you look at the zero, this is computed via three by three convolution. And so, it depends only on this three by three inputs grid or cells. So, it is as if this output units on the right is connected only to nine out of these six by six, 36 input features. And in particular, the rest of these pixel values, all of these pixel values do not have any effects on the other output. So, that's what I mean by sparsity of connections. 

Translation invariance - is addressed by CNN (shifted pixels is still identified by the filter)


### Shrinking number of channels
Pooling layers shrink - h and w
1x1 conv layers shrink the number of channels (Network in Network paper) --> can be used on MAXPOOL layer to reduce the # of channels.

### Bottleneck layer
Adding a 1x1 conv layer reduces computation cost, by acting as a **bottleneck layer**, without much loss in information.

### MobileNet (Depthwise Seperable Convolution)
Normal Conv - 
    for one output layer
        [n x n x n_c_prime] * [f x f x n_c_prime] to get the output [n_out x n_out] --> this is for one layer --> this needs (f x f x n_c_prime x n_out x n_out)
    **for all output layers, all filters have to be applied -> Remember each filter act as a block operation to create one output layer** 
        [n x n x n_c_prime] * [f x f x n_c_prime] x [n_f] to get the output [n_out x n_out x n_f] -> This needs (f x f x n_c_prime x n_out x n_out x n_f)

Output shape of Normal conv - [n_out x n_out x n_f]

f -> size of one filter
n_f -> number of filters
n_c_prime -> number of channels

In normal conv, every filter is applied to every block, not just one layer at a time.

Recall, that conv takes each filter and perform multiplication for that block and then does the same for each output unit needed.

**Depthwise seperable** has two steps
Depthwise uses single channel filter [3 x 3] instead of multiple channel filter and use number of filters same as input channels. 

> so n_f is set equal to n_c_prime

Depthwise - 
    for one output layer
        [n x n] * [f x f] to get the output [n_out_d x n_out_d] --> This is for one layer --> Takes (f x f x n_out_d x n_out_d)
    for all output layers
        [n x n] * [f x f] x [n_f_prime] to get the output [n_out_d x n_out_d x n_f_prime] -> This needs (f x f x n_out_d x n_out_d x n_f_prime)

n_out_d --> output of depthwise step

n_f_prime --> number of filters for depthwise is equal to the number of input channels --> this is fixed --> so n_f_prime is set equal to n_c_prime

Output shape of Depthwise step - [n_out x n_out x n_f_prime]

> Note: the filter is specially constructed as **not 3 x 3 x n_c, but 3 x 3**, since the conv layer has single layer filters and number of filters is equal to the number of input channels 

So red filter, performs the 3 x 3 multiplications and creates the n_out[0][0], then green filter creates n_out[1][1]

Pairwise - takes the input from Depthwise Output --> performs the operation on a **block**
    for one output layer
        [n_out_d x n_out_d x n_f_prime] * [1 x 1 x n_f_prime] to get the output [n_out x n_out] -> This needs (1 x 1 x n_f_prime x n_out x n_out) -> (1 x 1 x n_f_prime) for one spot
    for all output layers
        [n_out_d x n_out_d x n_f_prime] * [1 x 1 x n_f_prime] x [n_f] to get the output [n_out x n_out x n_f] -> This needs (1 x 1 x n_f_prime x n_out x n_out x n_f)  


**Pairwise applies the conv as a block on all channels, unlike depthwise which does layerwise.**

> the idea is to use the number of channels as filters in depthwise and create an intermediate layer. Then use original required number of filters in pairwise to get back the intended filter effect. For example, the n_c_prime input image channels is morphed to n_f_prime (not n_f which is the intended output) in the depthwise step. then the n_f_prime is changed to n_f in the pairwise step.

Normal Conv = (f x f x n_c_prime x n_out x n_out x n_f)
Depthwise + Pairwise = (f x f x n_out_d x n_out_d x n_f_prime) + (1 x 1 x n_f_prime x n_out x n_out x n_f)



### Efficient Net
If you are ever looking to adapt a neural network architecture for a particular device, look at one of the open source implementations of EfficientNet, which will help you to choose a good trade-off between r, d, and w.