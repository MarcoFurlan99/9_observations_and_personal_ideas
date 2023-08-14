# Crucial observations on the ideas we've worked with

We are taking latent spaces from our U-Net and interpreting them as probability distributions. More specifically, a latent space is a 4-dimensional tensor of dimensionality $(B, C, W, H)$, where:

- $B$ is the number of batches,

- $C$ is the number of channels,

- $W$ is the width,

- $H$ is the height.

Let us take as example the last latent space: this latent space has dimensionality $(1,4,4,1024)$ when the batch size is 1 and the input images have size 64x64. Now what we've been doing so far is interpreting such a tensor as a 1024-dimensional distribution, with a number of samples equal to 4x4xN, where N is the number of images. For instance, if N = 1000, we have 16000 samples in a 1024-dimensional space.

I was in the process of questioning this interpretation. Specifically:

- Why are we interpreting the tensors as probability distibutions?

- Why specifically interpreting them as 4x4xN samples in a 1024-dimensional space?

## Why are we interpreting the tensors as probability distibutions?

As a matter of facts, so far the two reasons I understood for such an interpretation are the following:

1. In [this paper](https://arxiv.org/pdf/1810.05148.pdf) they show that "Bayesian Deep Convolutional Networks [...] are Gaussian Processes". I'm still in the process to understand what a *Bayesian* DCN is and what a *Gaussian process* is. Furthermore they show that "the <ins>top-layer</ins> pre-activations [...] converge in distributionto an [...] normal vector [...] as $\min \lbrace n^1, ..., n^L \rbrace \xrightarrow[] \infty$

