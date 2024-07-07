# Attention Mechanism

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

In the last lesson, you learned to use encoder-decoder to translate a sentence. But sometimes, a sentence that is being translated might not perfectly align with the translated sentence at each time step. Here’s an example, take the sentence “Black cat ate the mouse.” In this example, the first English word is “black”, and the first French word is “chat ”, which means “cat” in English. How can you train the model to focus more on the word “cat” instead of the word “black” at the first time-step? In a translation model, the intuition behind the attention network is that it allows a neural network to only focus on part of an input sentence while it generates a translation, much like a human translator would do. To improve the translation, you can add the attention mechanism to the encoder-decoder.

In the traditional RNN encoder-decoder, the encoder only passes the final hidden state to the decoder.

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

An attention model differs from a traditional sequence-to-sequence model in two main ways. First, the encoder passes a lot more data to the decoder. Instead of passing the last hidden state of the encoding stage, the encoder passes all the hidden states to the decoder.&#x20;

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Second, an attention decoder takes an extra step before producing its output. To focus only on the most relevant parts of the input, the decoder does the following: First, it looks at the set of encoder hidden states that it received. (each encoder hidden state is associated with a certain word in the input sentence). Second, it gives each hidden state a score. Third, it multiplies each hidden state by its soft-maxed score, thus amplifying hidden states with high scores, and downsizing hidden states with low scores.

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Let’s now connect all the pieces together: The attention decoder of an RNN takes in the embedding of the token, and an initial decoder hidden state.

The RNN processes its inputs; producing an output and a new hidden state vector (H4). The output is discarded. Attention step: you use the encoder hidden states and the H4 vector to calculate a context vector (a4) for this time step. You concatenate H4 and a4 into one vector. You pass this vector through a feedforward neural network (one trained jointly with the model). The output of the feedforward neural networks indicates the output word of this time step. Repeat for the next time steps. After using the attention mechanism to modify the traditional encoder-decoder, you see an improvement in the translation.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>
