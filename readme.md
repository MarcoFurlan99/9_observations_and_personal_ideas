# Crucial observations on the ideas we've worked with

We are taking latent spaces from our U-Net and interpreting them as probability distributions. More specifically, a latent space is a 4-dimensional tensor of dimensionality $(N, C, W, H)$, where:

- $N$ is the number of images per batch,

- $C$ is the number of channels,

- $W$ is the width,

- $H$ is the height.

Let us take as example the last latent space: this latent space has dimensionality $(1,4,4,1024)$ when the batch size is 1 and the input images have size 64x64. Now what we've been doing so far is interpreting such a tensor as a 1024-dimensional distribution, with a number of samples equal to $4 \times 4 \times N_{Img}$, where $N_{Img}$ is the number of images. For instance, if $N_{Img} = 1000$, we have 16000 samples in a 1024-dimensional space.

I was in the process of questioning this interpretation. Specifically:

- Why are we interpreting the tensors as probability distibutions?

- Why specifically interpreting them as $4 \times 4 \times N_{Img}$ samples in a 1024-dimensional space?

## Why are we interpreting the tensors as probability distibutions?

As a matter of facts I have shaky reasons to justify this, the two main ones are the following:

1. In [this paper](https://arxiv.org/pdf/1810.05148.pdf) they show that "Bayesian Deep Convolutional Networks [...] are Gaussian Processes". I'm still in the process to understand what a *Bayesian* DCN is and what a *Gaussian process* is. Furthermore they show that "the <ins>top-layer</ins> pre-activations [...] converge in distribution to a [...] normal vector [...] <ins> as </ins>$\underline{\min \lbrace n^1, ..., n^L \rbrace \xrightarrow[]{} \infty}$.

2. this interpretation enables us to use distances between probability distributions, such as Bhattacharyya, KL-divergence, FID and Wasserstein (rather than being limited to distances between tensors, such as L^1, which in any case should be tried first for good measure and to set a baseline). Specifically the FID (Fréchet Inception Distance) is used commonly to evaluate the distance between generated images and target images in GANs (from  [this](https://machinelearningmastery.com/how-to-implement-the-frechet-inception-distance-fid-from-scratch/), "The Frechet Inception Distance, or FID for short, is a metric for evaluating the quality of generated images and specifically developed to evaluate the performance of generative adversarial networks.", "[the FID] captures the similarity of generated images to real ones better than the Inception Score").

## Why specifically interpreting them as $4 \times 4 \times N_{Img}$ samples in a 1024-dimensional space?

This is a very delicate point because I'm pretty sure it's just a completely wrong approach. In fact, **we should interpret the tensor as a 4x4-dimensional probability distribution, with $1024 \times N_{Img}$ samples**. Here are the reasons for this:

- When we compute the FID between images, <ins>as far as my understanding goes</ins>(based on [this](https://wandb.ai/ayush-thakur/gan-evaluation/reports/How-to-Evaluate-GANs-using-Frechet-Inception-Distance-FID---Vmlldzo0MTAxOTI)), we are computing mean and variance on the [???]

- [from [this paper](https://arxiv.org/pdf/1810.05148.pdf) the conclusion of Gaussianity is for the TOP-LAYER PRE-ACTIVATIONS w.r.t. width and height]

