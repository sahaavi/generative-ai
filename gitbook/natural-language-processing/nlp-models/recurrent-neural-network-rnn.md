# Recurrent Neural Network (RNN)

<figure><img src="../../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

In a DNN, the information flows through one direction from the input layer, to the hidden layers, and to the output layer. 01:02 This type of network is called feedforward neural network (FNN), and it’s where the information always moves in one direction and never goes backwards. 01:11 A feedforward-only network doesn’t really have a memory due to the one-way information flow. 01:15 The information that was previously learned doesn’t participate in predicting the next.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

Think about a sentence: He grew up in the United States of blank. If the sentence ends here, you can easily guess that the next word is America. To predict what comes after the previous words, a machine is expected to have some memory like a human.

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

An RNN is different from a DNN. It creates a recursive mechanism and lets the information pass to the next learning iteration in the same way it would “pass a memory.” Let’s look at how it works. Think about a DNN that includes an input layer, several hidden layers, and an output layer.

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

You compress the layers and flatten the figure.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

You obtain three elements: a green diamond to represent the input layer, a blue rounded rectangle to represent the hidden layers, and a yellow circle to represent the output layer. If you imagined a three-dimensional space, you would have numerous neurons behind these three symbols.

If you turn the figure counterclockwise 90 degrees, you’ll get the typical visual representation of an RNN.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

You must notice immediately that an extra loop points to the hidden layer itself. This is where the magic happens in an RNN. The loop carries the hidden states, which contain the memory, to the next time step of learning.

Imagine that an RNN is a chain of the same networks connected by the hidden states. These networks can be either a single hidden-layer ANN or a multiple hidden-layer DNN, and they pass a message to themselves at the next time step. In an RNN, xt-1, xt,, xt+1 , until xn represent the input at time t. yt-1, yt,, yt+1 , until yn represent the output. And ht-1, ht,, ht+1 , until h n represent the hidden state.

<figure><img src="../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption></figcaption></figure>

Inside each cell of a standard RNN, there’s a single neural network layer, tanh. An RNN normally takes one word at a time. The input of each cell is a concatenation of the hidden state ht-1, which carries the information from the previous iterations, and the input Xt. , which is a new word in a sentence. It then goes through a neural network layer tanh.

<figure><img src="../../.gitbook/assets/image (43) (1).png" alt=""><figcaption></figcaption></figure>

The tanh layer decides what information should pass to the next iteration. The output goes to two directions, one leads to the output yt after another hidden layer (or hidden layers). For example, you can feed ht to a dense layer followed by a linear layer and turn ht to the final output yt at time t. The other becomes the new hidden state ht, which will concatenate with the next input word Xt+1 to predict the output word Yt+1at the next time step. The hidden state is the messenger who carries all the prior information and travels to the next iteration.

<figure><img src="../../.gitbook/assets/image (44) (1).png" alt=""><figcaption></figcaption></figure>

An RNN normally feeds one word at a time. The new input word the concatenates with the hidden state ht-2, which carries all the previous information, to predict the output word united. At the same time, the RNN generates a new hidden state ht-1 and uses it to pass the memory to itself at the next time step. Then a new input word united concatenates with the hidden state ht-1 to predict the output states. And a new word states concatenates with the hidden state ht to predict the output of, and so on.

<figure><img src="../../.gitbook/assets/image (45) (1).png" alt=""><figcaption></figcaption></figure>

From the sentence perspective, an RNN model can predict the next word from given words. For example, an RNN remembers the and relies on it and all the previous words to predict the next word United. Then it uses the and United to predict States, and the, United, States to predict "of." Finally, by remembering the previous words the, United, States, and of, it’s easy for an RNN to decide that the next word is “America”. Because they are equipped with a memory, it's not surprising that NLP models are so smart!

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

### RNN Applications

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

### Limitations

As RNN operates timestep by timestep manner so they have very fundamental limitations.&#x20;

The first is that, to encode long sequences the memory capacity is effectively bottlenecking our ability to do that. That means information in very long sequences  can be lost.&#x20;

As we have to look at each slice in that sequence one by one, it can be really slow and computationally expensive to do this.&#x20;

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

### Goal

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

## Resources

\[The Unreasonable Effectiveness of Recurrent Neural Networks]\([https://karpathy.github.io/2015/05/21/rnn-effectiveness/](https://karpathy.github.io/2015/05/21/rnn-effectiveness/))
