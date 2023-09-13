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

