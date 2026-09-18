# SVD Image Compression Report

- Image 1 (Sea):
  Source: Magnific – Tropical Beach Sunny Day
  URL1="https://raw.githubusercontent.com/premlatamd/week02/refs/heads/main/images/sea2.jpeg"
  Licence: Magnific Standard Licence
  
- Image 2 (Crowd):
  Source: Nordic Monitor (X/Twitter post)
  URL2="https://raw.githubusercontent.com/premlatamd/week02/refs/heads/main/images/crowd.jpeg"
  Licence:licence not specified
  
- Image 3 (Saami):
  Source: Personal 
  URL3="https://raw.githubusercontent.com/premlatamd/week02/refs/heads/main/images/saami.jpeg"
  Licence: Captured by me


## Images Used

- Sea Image (Smooth Natural Scene)
- Crowd Image (Highly Detailed Scene)
- Saami Image (Moderately Detailed Image,This image is personal image)
  
---

# R6 – Written Analysis

## What SVD Produces and What Singular Values Mean

Singular Value Decomposition (SVD) breaks an image matrix into three matrices:

A = UΣVᵀ

When we applied SVD to an image, we got a list of singular values.

The first few singular values were very large,while the remaining values became smaller and smaller.

This means that most of the important information of the image is stored in the first few singular values.The smaller singular values mostly contain very fine details that are less noticeable to our eyes.

Because of this, we can keep only the first k singular values and remove the remaining ones.Even after removing many singular values,the reconstructed image still looks similar to the original image.

We store only the most important information and reduce the amount of data that needs to be saved.
...

## Measurement Method

For every image and every value of k,we measured:

- Compression Ratio
- Relative Error
- Energy Retained

The storage count for rank-k SVD is:

k(m + n + 1)

because we store:

- k columns of U
- k singular values
- k rows of Vᵀ

Compression Ratio:

mn / (k(m+n+1))

...

## Comparison Across Image Types

After applying SVD,we obtained a set of singular values.

We can think about singular values as indicators of how much information each component contributes to the image.

Larger singular values represent the most important visual information,while smaller singular values represent finer details and small variations.

This is why we can keep only the first few singular values and still reconstruct an image that looks similar to the original one.

### Sea Image

We observed that the Sea image compressed best.

When we looked at the Sea image,we noticed that most parts of the image looked very similar.Large areas of water and sky do not change much from one location to another.

Because of this,SVD was able to represent most of the image using only a small number of singular values.Even at lower values of k,the reconstructed image still looked very close to the original image.

### Saami Image

The Saami image contains more texture and edges than the Sea image.Therefore,it requires more singular values to preserve important features.

### Crowd Image

The Crowd image contains many people and fine details.Information is spread across many singular values,making compression more difficult.

Therefore:

Sea → Best Compression

Saami → Moderate Compression

Crowd → Lowest Compression
-------

## Choosing k

We selected k by three approaches:

1. Energy Threshold
2. Elbow Method
3. Relative Error below 5%

Among all the methods, we found that using reconstruction error was the easiest and most practical way to choose k.

We selected the smallest value of k for which the error became less than 5%. This allowed us to keep good image quality while still achieving compression.

### Limitation

One limitation of this method is that there is no single error threshold that works for every image.

Some images may still look visually good even with a higher error while other images may lose important details even when the error is relatively small.

Therefore, numerical measurements alone are not always sufficient.It is also important to visually inspect the reconstructed image before selecting the final value of k.

------


## Gaussian Noise Experiment

We added Gaussian noise to the Sea image at two different levels.

After adding noise, the singular value spectrum became flatter and the smaller singular values increased.

This indicates that noise spreads information across more singular values, making the image harder to compress.

At the same time, it shows why SVD can be used for denoising. By keeping only the dominant singular values and discarding smaller ones, a large amount of noise can be removed while preserving the main image structure.
---------
## Why SVD Compression is Not a Good idea.

SVD compression does not work very well for images that contain a lot of details, textures, or random patterns.

In our project,the Crowd image is a good example.The image contains many people,edges, and small details.To preserve these details,we need to keep a large number of singular values.

As the value of k increases,the amount of data that needs to be stored also increases.In such cases,the compression benefit becomes much smaller.

Therefore, SVD is usually more effective for smooth images and not so good for highly detailed  images.
----------

### R4 - important thingss about Energy Threshold

While using the energy threshold method,we noticed that it can sometimes give misleading results.

Many images have an overall brightness level.Because of this,the first singular value can become very large and may contain a large percentage of the total energy.

As a result,the 90% or even 99% energy threshold may be reached with a very small value of k.However,this does not always mean that the reconstructed image contains enough visual detail.

The energy is sometimes dominated by overall brightness rather than actual image features.

If we subtract the mean intensity from the image before computing the SVD (centering the image), the singular values become more representative of the real image structure. In that case, the required value of k may increase.

Therefore, energy retention should not be used alone.It is better to compare it with the elbow method and reconstruction error before selecting k.
-------

## R5 main points which is mentioned in question.

From our results,we can noticed that the type of images effects very much in SVD compression.

The Sea image does not needed more singular values ,as it does not contain fine details and other hand crowd & saami image contain more details so it needed more singular values for reconstructions.

We also observed that adding noise increased the smaller singular values and made compression less effective.
