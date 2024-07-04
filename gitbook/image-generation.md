# Image Generation

## Image generation model families

**Variational autoencoders (VAEs):** Encode images to a compressed size, then decode them back to the original size while learning the distribution of the data.

**Generative adversarial models (GANs):** Pit two neural networks against each other. One neural network the generator creates images and the other neural network the discriminator predicts if the image is real or fake. Overtime, the discriminator gets better at distinguishing real and fake and the generator gets better at real looking fakes.

**Autoregressive models:** Generate images by treating an image as a sequence of pixels. The modern approach with autoregressive model actually draws much of its inspiration from how LLM handles text.

**Diffusion model:** Diffusion models draw inspiration from physics specifically thermodynamics and they first introduced for image generation in 2015.

Diffusion models show promise across number of different use cases:

Unconditioned generation:  Unconditioned diffusion models which models have no additional input or instruction can be trained on image of specific thing to generate image of that thing such as faces. Another example of unconditioned generation is super resolution - increasing image quality.

Conditioned diffusion models give us thing like text to image, generating image from a text prompt and image editing and customizing an image with text prompt.

Let's see the Unconditioned generation:

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

The goal is that by training a model to denoise that model would be able take pure noise and from it synthesize a novel image. Let's break it down.

<figure><img src=".gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

We start a large dataset of images. Let's tale a single image start the forward diffusion process from $$x_0$$ the initial image to $$x_1$$the initial image with a bit of noise. We can do it over and over again iteratively to add more and more noise to the image. This distribution we call $$q$$ and it only depends on the previous step.&#x20;

<figure><img src=".gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

We can do it over and over for adding more noise. Ideally, once we do this for high enough $$T$$, we have reached the state of pure noise. The initial research paper implemented this with $$T=1000$$. Now we want to do this in reverse. How can we go from $$X_T$$ noisy image to $$X_{t-1}$$ less noisy image? Each step of the way, we also learn the reverse diffusion process - that is we train a machine learning model that takes input the noisy image and predicts the noise.

Let's take a look at the training step of this model.

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

We have our initial image $$X$$and we sample a timestep $$t$$ to create a noisy image. We train a denoising model to predict the noise. This model is train to minimize the difference between predicted noise and the actual noise added to the image. In other words, this model is able to remove noise from real images.

<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

To generate an image we can start with pure noise and send it through our denoising model, we can then take the predicted noise and subtract it from initial noise. If we do this iterativly over and over then we end up with generated image.

Another way to think about this, is that the model is able to learn the real data distribution of the images that it has seen and sample from that distribution to create new novel images. &#x20;

<figure><img src=".gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

