# Generative Modeling

**Goal:** Take as input training samples from some distribution and learn a model that represents that distribution.

That's means we try build Density Estimation models.

These models are going to see a bunch of different samples of data and they're going to learn to try to fit a function that models the probability distribution associated with how those data fall in some space.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

The other thing that we can do is we can take this learned distribution - this learned probability density - and then try to draw new samples from it. Can I use this sort of sampling operation to actually generate new data instances and this is this notion of sample generation.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

The common point to both these use cases of generative modeling is this question of how can we learn a very good model of the probability distribution that is similar to the true probability distribution of our real data.

Another use case of these generative model is outlier detection.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### Latent Variable Models

In statistics, latent variables are variables that can only be inferred indirectly through a mathematical model from other observable variables that can be directly observed or measured.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Our goal with generative models and latent variable models is to try to learn in an automated way something about a distribution that hopefully captures underlying drivers or factors that are resulting in the observed data that we see.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

To get at a sense of how we can do this from a deep learning neural network architecture framework we're going to start by talking about a really simple generative model that we call an autoencoder and the notion here is that we can take data and try to learn a lower dimensional encoding some set of features that hopefully represents that data faithfully.

#### Autoencoders

Here is an example with an image of the digit 2. The autoencoder is taking examples of this data and trying to learn a lower-dimensional feature space that represents it in a completely unlabeled way.&#x20;

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

So, let's ask ourselves: if we're trying to learn an encoding, which I denote as variable Z, why would we want to ensure that this set of variables Z has a fairly low dimensionality? To eliminate redundancies, exactly! Other benefits include efficiency. The concept here is to eliminate redundancy while being efficient, compressing the data to a lower-dimensional encoding that captures a rich representation of the data.

Now, the question is, how can we train a model to learn that lower-dimensional encoding? The concept of the autoencoder is to start with high-dimensional data, like an image, and compress it down to lower-dimensional data. We can use reconstruction of the data as an unsupervised task to teach the model to learn this encoding. The autoencoder takes an image, compresses it down to a lower-dimensional encoding space, and then performs decoding back up to the original data space's dimensionality. Effectively, you're learning a lossy reconstruction between your input data and the predicted reconstruction, which we're calling X hat.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Because this reconstruction is imperfect relative to the original data, we can train the network by comparing the input data X and the reconstruction X hat, and simply asking it to learn to minimize the difference between the two. This is done using the mean squared error, which with an image means comparing pixel by pixel in the image what the difference is between the original data X and the reconstruction X hat. So, this is a very straightforward way, and importantly, notice that in this reconstruction operation, our loss is only dependent on the input data X and the reconstruction X hat; there are no labels here.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

The final step, shown schematically, is to abstract away individual layers like convolutional layers, illustrating the concept of autoencoding. The input data is compressed into a lower-dimensional latent space (Z) and then decoded back to the original data space via reconstruction. This is a powerful idea, allowing the network to learn a feature set that hasn't been directly observed. Instead, the set of latent variables (Z) is entirely learned by the network, and our hypothesis is that it's effective enough to reconstruct the data accurately.

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

When it comes to the dimensionality of the latent space Z, a helpful way to think about it is in terms of orthogonality, memory bottleneck, and compression. The size of the latent space determines the quality of reconstructions and generations. The smaller the latent space, the more significant the memory bottleneck, resulting in greater loss and poorer reconstruction quality. There's a trade-off between the quality of samples and the size of the latent space.

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

The core concept of autoencoding is that we're forcing the network to learn a compressed latent representation by reconstructing the original data through a reconstruction loss. This process captures as much information about the data as possible, effectively enabling the network to learn to decode and recreate the data. This idea is where the name autoencoding comes from, and can be thought of as self-encoding or automatically encoding the data. The same concept of autoencoding down to a bottleneck latent layer is the foundation for generating new samples. To do this, we'll explore the concept of variational autoencoders, which will allow us to introduce more power and flexibility in our ability to generate new samples.

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Variational Autoencoders (VAEs)

Traditionally, the reconstruction process we just saw in autoencoder is a deterministic operation. The latent encoding Z is like any other neural network layer, meaning that once the network is trained and the weights are finalized, the same input will always produce the same reconstruction. This is not useful for generating new samples, as the network has only learned to reconstruct. To introduce variability and sampling, we need to add randomness and a probability distribution to the network. This is achieved through the concept of stochasticity or sampling in the network itself, which is the key difference between a variational autoencoder and a standard autoencoder. Instead of learning the latent variables directly, we learn the means and standard deviations for each latent variable, effectively defining a probability distribution for each one. This means we've gone from a vector of latent variables Z to a vector of means mu and a vector of standard deviations Sigma. This adds a probabilistic twist to autoencoding, allowing us to learn latent variables defined by a mean and standard deviation, and hopefully use this to sample from those probability distributions and generate new data instances.

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Now, let's dive deeper into the Variational Autoencoder (VAE) framework. Instead of a purely deterministic setup, we have two halves: the encoder (shown in green) and the decoder (shown in purple). The encoder takes the data and computes a representation of a probability distribution over the latent variables given the data X. The decoder does the inverse, operating on the latent variables to learn the distribution of the data X. These two networks, the encoder and decoder modules, are defined by their own sets of weights: Φ (phi) represents the weights for the encoder component, and Θ (theta) represents the weights for the decoder component.

To optimize the VAE, we need to define a loss function and objective. This loss function comprises two components. The first is the reconstruction loss, similar to the autoencoder loss we introduced earlier. This loss measures the difference between the input data X and the reconstructed data X hat.&#x20;

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

The second component is a regularization term, which introduces a prior probability distribution over the latent variables Z, defined by mu and sigma. This term measures the distance between the learned distribution q (inferred by the encoder) and our assumed prior distribution, such as a normal distribution. By comparing the learned distribution to our prior assumption, we can regularize the encoder to produce latent variables that match our expectations. The regularization term encourages the learned distribution to match our assumed prior distribution, effectively capturing the distance between the two distributions. This allows us to learn a representation that is not only reconstructive but also probabilistically meaningful.

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

**How do we choose that prior distribution?**

We need to choose a prior distribution for the latent variables. The most common choice in practice is to assume a normal distribution (Gaussian) as the prior, which means we assume each latent variable has a mean of zero and a standard deviation and variance of one. This encourages the model to distribute the encodings of the latent variables evenly around the centered latent space. We can further penalize the network when it deviates too far from this prior. The regularization term uses the Kullback-Leibler (KL) Divergence, a distance function that measures how closely two distributions match. When we use a normal distribution as the prior, the KL Divergence takes a simple form, shown here. Conceptually, we're trying to minimize the distance between the prior and the learned latent distribution, regularizing the network to match our assumed prior.

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Now, the question that's been raised a couple of times is: how do we choose this normal prior? Why do we choose it, and what does it effectively do? Let's break that down by considering what properties we want this technique of regularization to actually achieve.

The first idea is that we want our latent space to be continuous, meaning that points that are close together in this latent space zzz should be similar when decoded back into related content or images. For example, multiple different types of twos should be decoded into similar images.

Secondly, when we use our VAE to sample, we want completeness, meaning that whenever we draw a sample from the latent space, we should get something reasonable back out. We don't want samples to result in nonsensical outputs.

With these two criteria in mind, without regularization, we can sacrifice both properties. Things that are close in the latent space may not be similarly decoded, leading to a lack of continuity. For example, if we have a green point and an orange point close in the latent space, one might decode to a square and the other to a triangle, even though they are similar in the latent space. We want similar points to be close in the latent space.

<figure><img src=".gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Imposing regularization ensures that points close in the latent space are similar when decoded. This gives us a sense of why regularization is useful.

The normal prior helps us because, without this regularization, there isn't much structure in the distributions of the latent variables. Very small variances can lead to pointed distributions in the latent space, causing different means when sampled, which results in discontinuities. On the other hand, very large variances destroy any sense of difference when covering the latent space broadly.

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

Visually, without regularization, small variances and different means can lead to discontinuities. The high-level intuition with the normal prior is that it imposes regularization to be roughly centered with mean zero and standard deviation of one. This encourages the network to satisfy the desired properties of continuity and completeness.

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

How do we actually train this model end-to-end to learn these sets of weights? We have a loss function comprised of the reconstruction term and the regularization term, and our goal is to learn these weights completely end-to-end using this loss function. There's a problem, though, and a bit of nuance here.

By introducing the notion of sampling and the mean and standard deviation terms, it's not immediately clear how to backpropagate when we want to capture something probabilistic. VAEs employ a clever trick to address this: they divert the sampling operation by reparameterizing the latent variable equation slightly so that we can train the model end-to-end.

<figure><img src=".gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Rather than saying that our latent variable z is directly the sample of a normal distribution defined by μ and σ, we offset all the randomness to another variable, ϵ. Our latent variables are now the sum of a fixed vector of means μ and a fixed vector of standard deviations σ scaled by ϵ, which is drawn from a prior normal distribution. This effectively captures the stochasticity we want from our sampling operation while allowing us to backpropagate through the model.

As a result, this effectively diverts the sampling operation away from the latent variable 𝑧, where we cannot directly backpropagate. Instead, we learn a fixed set of means and a fixed set of standard deviations, diverting the stochasticity to the variable 𝜖. This allows us to backpropagate gradients through the model and directly learn the latent variables via the mean and standard deviation vectors. This technique is called the reparameterization trick in VAEs and is ultimately the solution that allows the network to be trained end-to-end.

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

When it comes to understanding what the latent variables represent in a trained VAE, we can keep all variables except one fixed and incrementally change the value of that single latent variable. Then, we use the decoder to decode back to our original data space.

For example, with a face reconstruction, if we perturb a single latent variable, we can observe changes in the head pose or tilt of the face in the reconstructed image. This process shows that different dimensions or latent variables are encoding different features that are hopefully interpretable.

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Ideally, with the idea of orthogonality and feature learning, you want the latent variables to be as orthogonal and uncorrelated to each other as possible. This maximizes the amount of information your model learns across the latent variables.

This notion is called disentanglement and is a common focus when training VAEs. The goal is to separate distinct features into different latent variables. For example, in the case of face images, you would want one latent variable to represent head pose and another to represent a smile, ensuring these features are disentangled from each other.

<figure><img src=".gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

There is a straightforward solution to encourage disentanglement when training a VAE. By relatively weighting the reconstruction term and the regularization term, and tuning the relative strength of these two components of the loss function, you can promote disentanglement.

A slight variant of the VAE, called Beta-VAE, achieves this by placing a weight greater than one on the regularization term. This constrains the latent bottleneck, encouraging it to disentangle distinct variables. As a result, you obtain more interpretable and better-disentangled features with greater weights on the regularization term.

More details and the mathematical explanation of why this works can be found in the Beta-VAE paper. The concept is that by imposing stricter regularization, you can more strongly disentangle these variables.

<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

#### Generative Adversarial Networks (GANs)

GANs are more focused on this question of how can we just generate samples that are going to be very good sacrificing the the ability to decode and interpret a set of latent variables.

The idea behind GANs is to learn a transformation from something very simple, such as completely random noise, to the real data distribution. Instead of explicitly modeling these probability densities, we learn a model that can transform the noise distribution into the real data distribution. This allows us to generate samples that hopefully fall within the real data distribution.

<figure><img src=".gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

GANs initially introduced a lot of excitement with the idea of generating data from completely random noise, which seems kind of wild when you think about it. The intuition behind GANs is quite clever. The concept is to put two components of the network, the generator and the discriminator, in competition with each other, acting as adversaries.

The generator takes completely random noise and attempts to transform it into data that resembles the real data distribution. Initially, its generations are quite poor. The discriminator then evaluates these generated instances, comparing them to real data, and determines whether they are real or fake.

By linking these two together and training them jointly, the goal is to induce the generator to create better and better examples, eventually good enough to fool the discriminator. The discriminator, in turn, tries to get better at distinguishing between real and fake data. This competition leads to improved generation quality as the generator and discriminator effectively compete with each other.

4o

<figure><img src=".gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

To break down how this works - provides a strong intuition behind how GANs operate.

Consider points along a line. We have our generator on the right, which starts with completely random noise and tries to create imitations of data. The orange points represent these fake data samples drawn from noise.

The discriminator looks at these points, along with real data instances, and produces a probability indicating whether the data it sees is real or fake. Initially, the discriminator's predictions are not very accurate. However, as it trains on more examples, it starts increasing the probabilities for real data and decreasing them for fake data.

We continue this process, training the discriminator as a normal classifier model using real and fake instances until it can perfectly distinguish between them. At this point, the generator observes where the real data instances lie. The objective supplied to the generator is to move its samples closer to the real instances.

The generator then starts creating new samples that are closer to the real data. The discriminator evaluates these new samples, adjusting its probabilities once again. This iterative process repeats, with the generator continually moving its fake points closer to the real data, and the discriminator continually adjusting its evaluations.

Eventually, the fake data points almost overlap with the real data points. At this stage, the discriminator can no longer tell which points are real and which are fake. This indicates that the generator has succeeded in learning to generate samples that mimic the real data distribution.

<figure><img src=".gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

The framework of GANs revolves around a generator component that aims to create fake data instances to deceive the discriminator, while the discriminator tries to distinguish between synthesized fake instances and real examples. In training, the GAN's objective, or loss function, sets up these competing goals for the generator and discriminator. The ideal outcome of successful GAN training is where the generator can perfectly replicate the true data distribution, rendering the discriminator unable to classify instances accurately.

However, training GANs is notoriously challenging in practice. Achieving this optimal scenario is difficult, and over the years, numerous approaches have been proposed to stabilize GAN training. These include refining loss functions and employing various tricks to enhance stability. Despite these efforts, GANs remain a complex class of models to train effectively.

To improve GANs, ongoing research explores new methodologies and models that offer greater robustness, ease of training, and stability compared to traditional GAN frameworks. These advancements aim to address the inherent difficulties associated with training GANs and pave the way for more reliable and practical applications.

<figure><img src=".gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

To use a GAN for generating new instances, we utilize the generator component of the model. Here's how it works:

1. **Generating New Instances:** We start with points in a noise distribution (e.g., Gaussian noise) and pass them through the generator. This process involves sampling, which simply means selecting different points from the initial distribution of random noise.
2. **Transformation Concept:** The GAN learns an effective transformation from this initial noise distribution to a learned target distribution. Essentially, it learns how to map random noise into meaningful data instances that resemble the real data distribution.
3. **Traversing the Learned Distribution:** What's fascinating is that we can explore and traverse this learned distribution space. Different samples from the Gaussian noise will correspond to different locations or instances in the data world. The GAN's mapping allows us to navigate this transformation.
4. **Interpolation and Generation:** Through this transformation, we can interpolate between points in the Gaussian noise space. This means starting from one noise sample, making small changes or perturbations, and generating progressive and similar images across the target data distribution.
5. **Cool Results:** This capability leads to exciting outcomes where initial perturbations in the noise samples result in progressive changes across the generated data. It demonstrates the GAN's ability to create varied and coherent outputs based on its learned understanding of the data distribution.

In essence, GANs provide a powerful framework for generating diverse and realistic data instances by transforming random noise into meaningful samples that align with the characteristics of the original data distribution.

<figure><img src=".gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

GANs are indeed a fascinating framework, and they were used to generate the types of face images shown on slide one. Over time, various advancements in modeling have led to improved results with GANs. One notable area of progress involves enhancing control over the generative process.

Traditionally, GANs start with random noise as input to the generator. However, researchers have explored ways to condition the generative process on additional information. This additional information, often called conditioning factors or labels, can guide the generation of specific types of samples from the GAN.

For instance, instead of solely inputting random noise, we can also include other forms of conditioning information. This might include class labels (e.g., different types of objects or facial expressions), attributes (e.g., color, style), or even text descriptions. By conditioning the generator on these factors, we can influence and control the characteristics of the generated samples to align with the desired attributes or categories.

This approach not only enhances the flexibility of GANs in generating diverse outputs but also enables targeted generation of samples that adhere to specific criteria or conditions, making GANs a versatile tool in generative modeling.

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

#### Application of GANs

A core idea in generative modeling is the concept of paired translation, where pairs of inputs are considered, such as a scene and its corresponding segmentation map. Instead of the discriminator operating on single inputs, it is trained to distinguish between true pairs (e.g., a real image with its segmentation map) and fake pairs (generated image with segmentation map).

In practice, paired translation allows for various transformations. For instance, the generator can take an input like a segmentation map and generate a corresponding real-world scene. This approach is versatile and can be used to generate different perspectives, such as transforming street view maps to aerial views, altering images from day to night, converting between black and white and color, and more.

A common application of paired translation is in mapping tasks, where it facilitates the conversion between different representations, such as transforming between map views and aerial images, providing flexibility in generating and manipulating visual data.

<figure><img src=".gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

A closely related idea to paired translation is the concept of learning relationships between two related but unpaired data distributions. This is where the architecture of Cycle GANs comes into play. Unlike paired translation, where explicit pairs are given, Cycle GANs deal with instances from one domain and another domain without direct pairing.

The essence of Cycle GANs lies in imposing a cyclic loss that links the generator and discriminator of one domain to the other. This setup allows the model to learn mappings between these two distributions and ensures that transformations can occur between the domains and back, maintaining consistency.

For example, consider images of horses and images of zebras. In a Cycle GAN, the model learns a mapping from the horse domain to the zebra domain and vice versa. This means it can transform the appearance of a horse into zebra-like stripes. Additionally, environmental factors like the color of grass might also change, demonstrating a comprehensive transformation of the entire image distribution itself.

Cycle GANs are valuable in scenarios where explicit pairs are unavailable but relationships between data distributions need to be learned and transformed, offering flexibility in generating and manipulating diverse visual data.

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

This concept of now domain translation domain transformation gets at this notion that Gans are very effective ways to basically learn transformations of data distributions we can go from learning a transformation from gaussian noise to our Target data distribution or with cyclic Gans from one data space X to a Target data space Y and back right.

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>
