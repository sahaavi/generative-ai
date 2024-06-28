# Word2vec

**Intuition:**

* **Learning Vocabulary:**
  * **Elementary School Example:** When you read, you guess the meaning of new words from context and remember them.
  * **Contextual Clues:** For example, in the sentence "Capable lawyers with business acumen are valuable to any firm," an eight-year-old might guess that "acumen" means intelligence or sharp judgment based on the surrounding words.

**Word2Vec:**

* **Context-Based Prediction:**
  * **Idea:** Use the context to predict the meaning of a word, similar to how we infer meanings from surrounding words when reading.
* **Variants:**
  * **Continuous Bag-of-Words (CBOW):** Predicts the center word given the context words.
  * **Skip-Gram:** Predicts the context words given the center word.
  *

      <figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Let’s look at how these two algorithms work.&#x20;

### CBOW

Let’s go back to our favorite example, “A dog is chasing a person.” Assume you miss the center word chasing, and CBOW tries to use the context words, Dog, is, a, and person to predict the missing word.&#x20;

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

This is as intuitive as filling in a blank puzzle on a quiz. How does it work technically?

Let’s walk through the two primary steps: preparing the dataset and training the neural network.

* Step 1: prepare the training data.
  * You run a sliding window of size 2K+1 over the entire text corpus. Corpus\[Latin word] means a collection of words or a body of words.
  *

      <figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
  *   Let's say K=2. You start with the first word A. To run a 2K+1 window and K equals to 2, you have two words before and after the center word A. No words before A but two words after A. Therefore, the two words after A, dog and is, will be used to predict A, which is sometimes called the label word.

      <figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
  *   Then the window shifts to the second word dog as the center word. Dog will be predicted by the word A before it and the words is and chasing after it. Therefore, three words: a, is, and chasing will be used to predict the label word “dog.”

      <figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
  *   The same process continues till the last word person is the center word. Now the training data is ready.

      <figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
* Step 2: train the neural network - specifically a narrow neural network—to learn the embedding matrix.
  * Narrow means there’s only one hidden layer in this model instead of multiple hidden layers, as in a deep neural network.
  *   The goal is to learn the embedding matrix Ev\*d , where v is the size of the vocabulary and d is the number of dimensions.

      <figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

      For example in the sentence “A dog is chasing a person,” you have five different words: a, dog, is, chasing, and person. Therefore, v equals to 5. The value of d depends on the number of features that you want the neural work to learn to represent each word. It can be anywhere between one to four digits. Normally, when the number is larger, the model will be more refined; although it costs more computational resources. d is also a hyperparameter that you can tune when using Google’s pre-trained word2vec embedding, which means that you can try different numbers to see which one produces the best result. To make the visual simple, let’s say d equals to 3 here.

      <figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
  *   Therefore, the matrix in this example is 5 by 3 and it looks like this. Each w represents a weight that you want to train the neural network to learn.

      <figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
  *   A simplified version to explain the process is to take the vectors of the surrounding 2000 words as input, sum them up, and output a vector to represent the center word.

      <figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

      Let’s discuss this in more detail.

      <figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

      First is the input layer. The Input layer consists of 2000 words, each is represented by a one-hot encoder vector. If you recall from the previous lesson, a one-hot encoder is a one by v vector and v is the size of the vocabulary. You’ll place a 1 in the position corresponding to the word and zeros in the rest positions. Then you embed these vectors with the embedding matrix Ev\*d, which means you multiply each vector by the embedding matrix E.

      <figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

      To illustrate this, let’s assume you have an input vector of a one-hot encoder as \[0,1,0,0,0]. You multiply it with the embedding matrix, which in the case is the word2vec, by using the CBOW technique. And then you get the embedded 1\*d vector as \[10,12,23]. You can imagine the embedding matrix as a lookup table to turn the original word into a vector that has semantic meaning. To begin this process, all the values (weights) in the embedding matrix E are randomly assigned. Once you get the embedded vector for each context word, sum all the vectors and get a hidden layer H, a one by d vector. You multiply H with another matrix E’ and feed the result to a softmax function to get the probability y. y is a one-by-v vector and each value shows the probability of the word in that position being the center word. This is the output layer and the predicted result. However, this is actually the beginning of the iteration. You must compare the output vector with the actual result, And use backpropagation to adjust the weights in the embedding matrices E and E’. Iterate this process until the difference between the predicted result and the actual result is minimum. Now you get the E, the word2vec embedding matrix that you aimed to learn at the beginning. The training process depicts how a neural network learns.

### Skip-gram

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Opposite to continuous bag-of-words (CBOW), skip-gram uses the center word to predict context words. For example, given chasing, what are the probabilities of other words such as a, dog, and person occur in the surrounding context?

The process is similar to CBOW, though.

**Step1: prepare the training data**

First, you prepare the training data by running a sliding window of size 2K+1. For example, let k equals to 2.&#x20;

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

You start with the first word A. You have no word before A but two words after it. Therefore, you use A to predict dog and is respectively.&#x20;

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

And then the window shifts to the second word dog as the center word. You use dog to predict the word a before it and the words is and chasing after it.&#x20;

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

The same process continues till the last word person is the center word. Now your training data is ready.

**Step2: train neural network**

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Next, you train the neural network to learn the embedding matrix E. Compared to CBOW, E here is based on the skip-gram technique. You start with the input layer which consists of the one-hot encoder vector of the center word. Embed this vector with embedding matrix E, and feed the embedded vectors to one hidden layer. After another E’ and the softmax function, you finally generate the output layer which consists of vectors to predict 2000 surrounding context words.

**Coding**

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Keras in TensorFlow packages all the details and you only need to call the pre-trained models and tune the hyperparameters. In the setup you must import embedding from keras. Then you use one statement to create an embedding layer to embed the words in the vocabulary into certain dimensional vectors. The embedding layer can be understood as a lookup table that maps from specific words (integer indices such as one-hot encoder) to dense vectors (their embeddings). The dimensionality (or width) of the embedding is a parameter that you can experiment with to see what works well for your problem, much in the same way you would experiment with the number of neurons in a dense layer. When you create an embedding layer, the weights for the embedding are randomly initialized (just like any other layer). During training, they are gradually adjusted by using backpropagation. Once trained, the learned word embeddings will roughly encode similarities between words (as they were learned for the specific problem your model is trained on).

### Resources

\[Word Embedding and Word2Vec, Clearly Explained!!!]\([https://www.youtube.com/watch?app=desktop\&v=viZrOnJclY0](https://www.youtube.com/watch?app=desktop\&v=viZrOnJclY0))
