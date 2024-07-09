# Transformers

If you recall from module one, the recent breakthroughs in the past ten years include the usage of neural networks to present text such as word2vec and n-grams in 2013. In 2014, the development of sequence to sequence models such as RNN and LSTMs helped improve the performance of ML models on NLP tasks such as translation and text classification. In 2015, the excitement came with the attention mechanism and the models built based on it such as transformers and BERT. You’ll focus on Transformers in this lesson.

<figure><img src="../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

Although all the models before Transformers were able to represent words as vectors, these vectors remain constant and they don’t change based on context. For example, bank in river bank versus bank in bank robber have the same vector representation. To solve this problem, it’s essential to develop a text representation that considers the word context and a model that learns how certain words are aligned to each other. Attention mechanism helps improve the performance of machine translation applications.

Transformers are built based on the attention mechanism.

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

A Transformer model consists of encoder and decoder. The encoder encodes the input sequence and passes it to the decoder, which learns how to decode the representations for a relevant task. The encoding component is a stack of encoders of the same number. The research paper that introduced Transformers stacks six encoders on top of each other, so six is not a magical number; it's a hyperparameter. The encoders are all identical in structure; but with different weights.

Each encoder can be broken down into two sublayers: The first layer is called self attention. The inputs of the encoder first flow through a self-attention layer, which helps the encoder look at the relevant words as it encodes a center word in a input sentence. And the second layer is called feedforward. The outputs of the self-attention layer are fed to a feedforward neural network. The exact same feedforward neural network is independently applied to each position. The decoder has both the self attention and the feedforward layer, but between them is an encoder-decoder attention layer that helps the decoder focus on relevant parts of the input sentence.

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

After embedding the words in the input sequence, each of the embedding vector flows through the two layers of the encoder. The word at each position passes through a self-attention process. Then, they each pass through a feedforward neural network: the exact same network with each vector flowing through it separately. Dependencies exist between these paths in the self-attention layer. However, the feedforward layer does not have those dependencies, and thus the various paths can be executed in parallel while they flow through the feedforward layer.

<figure><img src="../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

As you encode the word "it" in say encoder #5 (the top encoder in the stack), part of the attention mechanism focuses on "The animal", and bake the representation into the encoding of "it."

<figure><img src="../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

For each word, you create a Query vector, a Key vector, and a Value vector. These vectors are created by multiplying the embedding by three matrices that you trained during the training process.

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

W matrices here are the learned weights. The dimensionality of the vectors is 64, although the embedding and encoder input/output vectors have dimensionality of 512. The vectors don’t HAVE to be smaller; this is an architecture choice to make the computation of multi-headed attention (mostly) constant.

<figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

What are the query, key, and value vectors? You'll see as you advance.

Once, we get the corresponding Q, K, V vectors for the input sentence. The next step is to multiply each value vector by the softmax score (in preparation to sum them up).

<figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

The intuition here is to keep intact the values of the word(s) you want to focus on, and leave out irrelevant words (by multiplying them by tiny numbers like 0.001, for example).&#x20;

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

Next, we have to sum up the weighted value vectors which produces the output of the self-attention layer at this position (for the first word). You can send along the resulting vector to the feedforward neural network.

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

This process improves the performance of the attention layer in two ways: It expands the model’s ability to focus on different positions. The final embedding from one encoder contains parts of other encoders but it could be dominated by the actual word itself. It gives the attention layer multiple “representation subspaces.” Each set is used to project the input embeddings (or vectors from lower encoders or decoders) into a different representation subspace.

The feedforward layer doesn’t expect eight matrices: It expects a single matrix (a vector for each word). So you need a way to condense these eight into a single matrix. How do you do that? You concat the matrices and then multiply them by an extra weights matrix Wo\[Wellsaid, please say w o].

<figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

To sum, this is the process of getting the final z embeddings.

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

So far, the model is missing a way to account for the order of the words in an input sequence. To solve this problem, the transformer adds a vector to each input embedding to encode the position. These vectors follow a specific pattern that the model learns, a specific pattern that the model learns, which helps determine the position of each word, or the distance between different words in the sequence.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

These encodings are called positional encodings and are combined with the embeddings of the word.

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>
