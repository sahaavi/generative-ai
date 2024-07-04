# Recurrent Neural Network (RNN)

In a DNN, the information flows through one direction from the input layer, to the hidden layers, and to the output layer. 01:02 This type of network is called feedforward neural network (FNN), and it’s where the information always moves in one direction and never goes backwards. 01:11 A feedforward-only network doesn’t really have a memory due to the one-way information flow. 01:15 The information that was previously learned doesn’t participate in predicting the next.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Think about a sentence: He grew up in the United States of blank. If the sentence ends here, you can easily guess that the next word is America. To predict what comes after the previous words, a machine is expected to have some memory like a human.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

An RNN is different from a DNN. It creates a recursive mechanism and lets the information pass to the next learning iteration in the same way it would “pass a memory.” Let’s look at how it works. Think about a DNN that includes an input layer, several hidden layers, and an output layer.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

You compress the layers and flatten the figure.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

You obtain three elements: a green diamond to represent the input layer, a blue rounded rectangle to represent the hidden layers, and a yellow circle to represent the output layer. If you imagined a three-dimensional space, you would have numerous neurons behind these three symbols.

If you turn the figure counterclockwise 90 degrees, you’ll get the typical visual representation of an RNN.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

You must notice immediately that an extra loop points to the hidden layer itself. This is where the magic happens in an RNN. The loop carries the hidden states, which contain the memory, to the next time step of learning.

Imagine that an RNN is a chain of the same networks connected by the hidden states. These networks can be either a single hidden-layer ANN or a multiple hidden-layer DNN, and they pass a message to themselves at the next time step. In an RNN, xt-1, xt,, xt+1 , until xn represent the input at time t. yt-1, yt,, yt+1 , until yn represent the output. And ht-1, ht,, ht+1 , \[WellSaid: h t minors 1, h t, x t plus 1, until h n] represent the hidden state.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

