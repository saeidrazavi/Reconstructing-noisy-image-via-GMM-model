# Reconstructing noisy image via GMM models
In this repo, we apply EM algorithm to find parameters of a GMM distribution of dataset, to infer ”clean” image from corrupted images (in this case, MNIST dataset). This process is known as ”Regularization Inverse Problem

## Implementation 
### Data Preparation
In the first step we need to extract numerous patches from each image. In order to do that,
consider a m × m square at the upper left corner of an image. This is the first patch of the
image. Next, sweep that square one pixel to the right. This is the second patch. We Continue
this until you we reach the upper right corner of the image. Then, place the square at the upper
left corner again, this time shift this corner one pixel down. Continue this procedure until we
sweep all the image and now you have extracted all of the patches (each m × m pixels), with
maximum overlap

### Denoising algorithm
We will assume that the distribution of patches (Z) is a GMM with K components.
In the next step, we are given some corrupted images as test dataset. These images are
corrupted by two methods, namely, blurring and additive noise. We will define Y as random
variable indicating corrupted patches. We know that each clean patch is corrupted by first
getting multiplicated by a blurring (wieght) matrix, W (which is attached in files) and then
we have added some normal noise to it. So we may infer that the conditional distribution of
corrupted images given a clean image is: 

$$p_{\boldsymbol{Y|Z}}(y|z)=\mathcal{N}(Wz+\sigma^{2}I)$$

Where $\sigma^{2}$ is variance of the added noise. We want to infer what the clean
image is after getting the noisy image so we have to calculate the posterior probability which
is proportional to multiplication of $p_{\boldsymbol{Y|Z}}$ and prior probability of patches $p_{\boldsymbol{Z}}$.

if we have normal prior distribution $p_{\boldsymbol{Z}}(z) = \mathcal{N}(\mu_{Z,Y}, Σ_{Z,Y})$ and normal
likelihood distribution $p_{Y|Z(y|z)} = \mathcal{N}(Wz + b, Σ_{Y|Z})$, we know that joint distribution will be
Normal and its parameters is as follows (note that by using both prior and marginal distribution we can calculate posterior distribution too): 

$$p_{Z,Y}(z, y) = \mathcal{N} (\mu_{Z,Y}, Σ_{Z,Y})$$

$$\mu_{\boldsymbol{Z,Y}} = 
\begin{bmatrix}
	\boldsymbol{\mu_z}\\
	\boldsymbol{b+W\mu_z}
\end{bmatrix}$$

$$\Sigma_{\boldsymbol{Z,Y}}=\begin{bmatrix}
\boldsymbol{\Sigma_{z}}&\boldsymbol{\Sigma_zW^T}\\
\boldsymbol{W\Sigma_z}	&\boldsymbol{\Sigma_{y|z} + W\Sigma_{z}W^T}
\end{bmatrix}$$

The goal of a denoising algorithm is estimating the clean image after seeing corrupted version
of it. So we need to calculate the MAP estimate for $p_{\boldsymbol{Z|Y}}$. Calculating the MAP estimation for
a GMM does not have a closed form solution. We use an approximation to find an estimated
solution for MAP of a GMM. We assume that the answer to this problem is that to first find the
component with maximum probability $(π_{k} · p_{\boldsymbol{Z|Y,K}}(z|y, k))$ and then find the MAP estimation
of $p_{\boldsymbol{Z|Y,K}}(z|y, k)$, which in case of a normal distribution, is equivalent to its mean.

## Results 
Below, you can see the results of our GMM model:







<p align="center">
  <img src="https://github.com/saeidrazavi/Reconstructing-noisy-image-via-GMM-model/assets/67091916/3b8c0c0d-769f-484c-94c1-cb5c1d7de2de" width="900" title="Results">
</p>
