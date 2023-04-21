🎯Learning 2: What really made a difference is layer-normalizing the outputs of Q and K in the attention block: `LN(Q(x))` and `LN(K(x))`.
This change was inspired by https://lnkd.in/e_Avsscd.
We also tried L2-normalizing the outputs of Q and K (following https://lnkd.in/eJ69fNUf); it gave a similar stability benefit, although with slightly worse downstream performance.