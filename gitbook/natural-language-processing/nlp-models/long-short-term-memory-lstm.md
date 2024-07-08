# Long Short Term Memory (LSTM)

<figure><img src="../../.gitbook/assets/image (41) (1).png" alt=""><figcaption></figcaption></figure>

He grew up in the United States of blank. If the sentence pauses here, an RNN model can easily guess that the next word is America based on the previous words right before it, which are, the, United, States, and of.

<figure><img src="../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

What if the paragraph continues till He speaks English. Can an RNN remember the country name far back from the beginning of the paragraph and use it to predict the language he speaks? Unfortunately, the answer is no. Although an RNN has a memory, it suffers from short-term memory. It only remembers nearby words. If you try to process a paragraph of text, an RNN might leave out important information from the beginning. So why does this happen? The problem is due to vanishing gradients.

Recall that in the previous lesson, you explored the fundamentals of an ANN (or a simple neural network). You have the loss/cost function to calculate the difference between the predicted result and the actual result. The cost function can be Mean Squared Error (MSE) for regression problems, or cross-entropy for classification problems. You then use the derivative of the cost function to decide the direction to adjust parameters, specifically weights and errors, for the backpropagation. After a couple of iterations, you achieve the minimum cost function and the optimum prediction. The gradient descent plays an important role to help you find the bottom (or regional minimum).

#### Vanishing Gradients

However, gradient descent has a problem. You might notice that toward the bottom, the ball moves slower than before because the derivatives are close to zero. The derivatives become too small to affect the adjustment of the parameters, which leaves weights and errors nearly unchanged, especially those in the earlier layers. This causes the model to stop learning or take too long to converge to the optimum. This problem is known as vanishing gradients.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

To put the problem into a practical perspective, it means that the closer words have a stronger effect on the prediction, whereas the further words have less impact.

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

The vanishing gradient leads to the short-memory of an RNN. This is a large issue that bothered researchers for a long time till the emergence of LSTM (short for long short-time memory). LSTM brings long-term memory to the NLP models.

Before exploring an LSTM cell, let’s recall what a basic RNN cell looks like. It has two inputs: Xt, which contains the input at time t. Ht-1, which is the hidden state that carries the information from the previous cells. Then you concatenate Xt and Ht-1 and pass them through a single tanh layer. This gives you the new hidden state Ht to pass to the next time step. Recall from the previous lesson, tanh is an activation function to convert a number to a value from -1 to +1.

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

Compared to an RNN, an LSTM adds new neural network layers and a few operations in a cell.

<figure><img src="../../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

The first difference to notice between an RNN and an LSTM cell is that an RNN has one pipeline, whereas an LSTM has two pipelines that go through the cell. That’s the critical improvement of LSTM over RNNs. Imagine that the pipeline represents the memory that goes through cells. An RNN has a short-term memory. However, an LSTM, in addition to the short-term memory, has a long-term memory!

<figure><img src="../../.gitbook/assets/image (6) (1) (1).png" alt=""><figcaption></figcaption></figure>

The second difference that you might notice is the different structures inside the cell. All the magic happens here.

Let’s first explain the symbols. Blue represents the four neural network layers added by an LSTM. Dark gray represents the pointwise operations including multiplication and addition. A straight line represents the vector transfer. All the inputs such as x, h, and c and the outputs such as y, c, and h are vectors. A join is a concatenation. And a fork means copy.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption></figcaption></figure>

The key to LSTMs is the cell state. Imagine it carries the long-term memory that runs through the entire network chain.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

The mechanism to regulate the flow of information is called gate. Gate consists of a sigmoid function and a pointwise multiplication function. Recall from the previous lesson that sigmoid is an activation function that turns a number to a value between 0 and 1. Zero means to forget the information completely and 1 means to remember the information entirely. The outcome after the sigmoid function then multiplies the original value on the pipeline. The result decides how much information to pass through to the next iteration. The mechanism works like a gate.

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

Considering gate, you can divide the neural network layers inside an LSTM cell into three sections. The first section has a forget gate. It decides what irrelevant information to forget. The second section has an input gate. It decides what new information should be remembered. The third section has an output gate. It decides what information should pass to the next time step.

<figure><img src="../../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

Let’s start with the first section. This is where an LSTM learns to forget. How does it work? From the bottom up, the hidden state ht-1, which carries the information from the previous time steps, concatenates with the input xt , and then passes through a sigmoid layer, 𝞋. The outcome of the sigmoid function is a vector that consists of values between 0 and 1. The values decide what information carried by the hidden state should pass to the next iteration. This outcome vector then moves up to multiply the cell state Ct-1. Ct-1 will be updated by deleting the irrelevant information. This is where an LSTM learns to forget.

The second section has an input gate. It includes two neural network layers: The first layer is to use a sigmoid function to filter the new information that must be added to the cell state. 2. The second layer is to use a tanh function to create a new candidate of the cell state. The input gate combines 1 and 2 and basically scales the new cell state by how much new information an LSTM decides to add. The outcome is then added to the cell state to update the long-term memory. This is where an LSTM learns to remember.

The third section has an output gate. It combines the input, the hidden state, and the cell state and decides what to output to the next time step. The benefit of creating a cell state pipeline is to let information pass through in a much straightforward way. No neural network layers are located on this pipeline other than pointwise operations such as multiplication and addition, which operate directly on numbers. For example, if the LSTM cell decides that the previous information is 100% irrelevant, it can turn off the valve at the forget gate. And if it decides that the new information is 100% useful, it turns on the valve to the maximum and adds to the cell state. In this case, the long-term memory forgets about what happened in the past and will only remember new information from now on.

This is how an LSTM works. It creates a cell state to pass the long-term memory and uses a hidden state to pass the short-term memory. It also applies a mechanism called gate to regulate the information flow.

## Resources

\[Understanding LSTM Networks]\([https://colah.github.io/posts/2015-08-Understanding-LSTMs/](https://colah.github.io/posts/2015-08-Understanding-LSTMs/))
