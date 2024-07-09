# Encoder-decoder architecture

Let’s say you want to translate an English sentence “The cat ate the mouse.” to French “le chat a mangé la souris” \<lu sha | a meng-she | la su-hei>. How can you train a neural network to do it? Well, here’s something you could do. First, you use a network called encoder. It can be built as an unrolled recurrent neural network (RNN), or other ML models such as a Long Short Term Memory (LSTM) and Gated Recurrent Unit (GRU), which were introduced in last module.

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

Then, you feed the English sentence one word at a time. Once ingesting the inputs into the RNN, you output a vector that represents the input sentence. After that, you build the other network called decoder. The decoder takes the outputs from the encoder network as its inputs.

<figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

When the model is given enough training data of pairs of English and French sentences, it actually works decently well.

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

A problem that does not have an easy solution is the softmax layer. If you compute word probabilities over the entire English vocabulary, let’s say 100 k English words, you need a softmax layer that outputs a vector of 100 k elements and each element typically comes with a range of 500 neurons. 100 k times 500, that’s 50 million weights to predict one word, wow, a BIG number!

<figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

For model predictions, you don’t have a choice. But for model training, the gradient is what interests you the most. Many techniques have been devised to compute gradients in an affordable approximate way. TensorFlow has implemented a couple of techniques to accelerate this process. For example, you can use the sampled\_softmax\_loss() method to compute and return the training loss.

<figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

After you feed the English sentence into the encoder, the encoded sentence becomes the input of the first RNN cell of the decoder. The input of this cell is some arbitrary “GO” token that marks the beginning of the sentence. For the predictions, you can simply call an embedding layer method to convert words into embeddings. Then, you add a Gated Recurrent Unit (GRU) layer. Y is a dense layer. With the softmax function, you can get the conditional probability of each word in the vocabulary. But how can you get the actual predicted word from those probabilities? The first idea is to do a “greedy search”, with which you generate the first word based on the highest probability. Once deciding the first word, you then pick the second based on the second highest probability and so on. \[animation - new parts appearing one by one] However, this approach does not produce the best translation.

<figure><img src="../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

The neural network provides the conditional probability of the next word by knowing what comes earlier at each time step of the decoding. A few algorithms can be used to predict the next word given its conditional probability. The most widely used one is called beam search. Instead of picking only one most likely word at each time step in the decoder network, like the greedy search does, beam search considers multiple alternatives at a time.

<figure><img src="../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>
