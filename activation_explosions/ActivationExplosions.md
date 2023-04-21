Learning 1: Activation explosions were good indicators that the loss would diverge.
`max(abs(.))`, L1 norm, L2 norm, etc., it doesn't matter, same trend.
The explosion is the strongest at the lowest layers. It would then propagate through the network.
We observed the same trend with both activations and gradients.

Activations and gradients explosions are a good indicator that the loss is going to diverge
We observed that activation explosions were strongly correlated with the loss diverging. In general, the activations would increase a lot (in L1 norm for instance), 100s of steps before the loss diverges… We observed the same behavior with gradients. This is particularly striking for a few modules: first, the outer projection activations (i.e. the output of the FC2 in the MLP block, and the O in the attention block), second and to a lesser extent, the Q and K in the attention, and third (to an even lesser extent) the V in the attention. This is particularly true in the early layers.


How do we measure Activation values

How do we address it
Layer Norms on the Q and K projections made a difference in taming these divergences
Inspired by the Scaling ViT to 22B parameters paper, we applied layer normalization right after the Q and K projections (i.e. `LN(Q(x))` and `LN(K(x))`), as they observed the same behavior with respect to activations exploding. I initially thought that having Q and K outputs increase significantly wasn’t that much of a problem because the softmax operation would bring things into [0, 1]. That was a wrong assumption.
We also tried L2 normalizing the Q and K outputs (following Q-K Normalization for Tfrms) and it yielded lower performance, although a similar stabilization boost.

Unsuccessful, but can be tried
Hyper-parameter sweep: LR, warm up steps, batch size, z_loss weight
Your typical “keep calm and decrease your LR”. Generally speaking, bigger batch size allows using bigger LR which means faster loss decrease (step wise, not flops wise).
Slack context
AdamW optimizer HP sweep: beta1, beta2, eps, weight decay
Close to no impact in our context.


Activations tracker
Very useful for debugging and monitoring: it is essentially hooks that attach to the forward and periodically track inputs/output activations (and also potentially weights). 
It was derived from Stas’ Under/Overflow utilities in HF Transformers. - https://github.com/huggingface/transformers/blob/64d95c44ec44e5f8d50b47cbcadb0471bf99ef17/src/transformers/debug_utils.py#L27
