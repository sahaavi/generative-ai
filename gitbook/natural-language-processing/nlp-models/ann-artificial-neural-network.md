# ANN (Artificial Neural Network)

An ANN is often called neural network (NN) or shallow neural network. Put simply, you have three layers in an ANN: an input layer, a hidden layer, and an output layer. Each node represents a neuron. The lines between neurons stimulate synapses, which is how information is transmitted in a human brain. Let’s use the lab as an example. The input layer includes text, or more specifically, the article titles from multiple resources, and the output layer shows the probability whether this article title belongs to different media: GitHub, NYTimes (short for the New York Times), and TechCrunch.

<figure><img src="../../.gitbook/assets/image (8) (1) (1).png" alt=""><figcaption></figcaption></figure>

How does an ANN learn from examples and make predictions?

<figure><img src="../../.gitbook/assets/image (10) (1) (1).png" alt=""><figcaption></figcaption></figure>

Let’s assume you have two input neurons or nodes, one hidden neuron, and one output neuron. Above the link between neurons, there are weights or parameters. The weights retain the information that a neural network learned through the process and they are the mysteries that a neural network aims to discover. The first step is to calculate the weighted sum, which equals to the total of the multiplication of input values and weights. It normally includes a bias component bi. However, to focus on the core idea, we’ll ignore it for now. The second step is to apply an activation function to the weighted sum. What is an activation function and why do you need it? Let’s pause your curiosity for just a moment and we’ll introduce the activation function in a few slides. For now, you must know that an activation function is used to prevent linearity. In the next two steps, the same process is applied to the output layer. The third step is to calculate the weighted sum assuming you have multiple neurons in the hidden layers. And the fourth step is to apply an activity function to the weighted sum. This activation function can be different from those applied to the hidden layers. The result is the predicted y, which consists of the output layer. You use y hat as the predicted result and y as the actual result.

Let's get back to activation functions. [activation-function.md](activation-function.md "mention")

Now that you understand the purpose of an activation function and its common types, what is the next step after the model generates a predicted outcome y? You might be a little disappointed so far, because nothing seems fancy and it’s all simple math. So, how does a neural network actually learn? Let’s ask you a question, how does a human learn? A human can learn fast from the past lessons. A neural network simulates that process and learns from its past performance in prediction. Here come the more interesting steps. Step five is to compare the predicted result y hat with the actual result y, and the goal is to minimize the difference. If the difference is significant, the neural network knows that it does a lousy job in prediction and must go back to learn more and adjust parameters. But how to quantify the difference between the predicted result y hat and the actual result y? You use a function called cost function or loss function. Cost function is used to compute errors of the entire training set, whereas loss function is used to calculate errors for a single training data instance.&#x20;

<figure><img src="../../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

Among different types of cost functions, mean squared error (MSE) is commonly used for linear regression problems. MSE equals to the average of the sum of squared differences between y hat and y. Cost functions used in classification problems are different than those in regression problems. Cross-entropy is commonly used.

<figure><img src="../../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

To skip the complex math, you only must know that cross-entropy has been used to calculate the differences between probability distributions. After you calculate the difference between the predicted result and the actual result, you go back to adjust weights or parameters to minimize the cost function. This step is called backpropagation. The challenge now is how to adjust the weights. The solution is slightly complex but it’s indeed the most interesting part of a neural network.

Do you remember the cost function to calculate the differences between predicted results and actual results? The idea is to take a cost function and turn it into a search strategy. That’s where gradient descent comes in.

<figure><img src="../../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

Gradient descent refers to the process of walking down the surface formed by the cost function and finding the bottom. It turns out that the problem of finding the bottom can be divided in two different and important questions: Which direction should you take? and How large or small should the steps be?

<figure><img src="../../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

The answer to the first question is the derivative. The derivative decides the direction to take. For example, let’s say you start from the top left. You calculate the derivative of the cost function and find it’s negative. That means the angle of the slope is negative and you are at the left side of the curve. To get to the bottom, the direction is to go down to the right.

<figure><img src="../../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>

Let’s say at one point you are on the right side of the curve, You calculate the derivative again. This time the value is positive and you must slide again to the left. You calculate the derivative of the cost function every time to decide which direction to take. Repeat this process, according to gradient descent, and you will eventually reach the bottom (or the regional bottom).

The second question is how large or small should the steps be? The step size depends on the learning rate, which determines the learning speed and how fast you bounce around to reach the bottom.

<figure><img src="../../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>

If the step size is too small, your training might take too long.

<figure><img src="../../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

If the step size is too large, you might bounce from wall to wall or even bounce out of the curve entirely, without converging.

<figure><img src="../../.gitbook/assets/image (38) (1).png" alt=""><figcaption></figcaption></figure>

If the step size is just right, then you’re set. Step size or “learning rate” is a hyperparameter that is set before training. The last step is to iterate this process.

<figure><img src="../../.gitbook/assets/image (39) (1).png" alt=""><figcaption></figcaption></figure>

The neural network continues adjusting weights or parameters until the cost function reaches the optimum. How do you know whether it reaches the bottom? Good question, you’ll know it when the value can’t go down anymore regardless of the training iterations.

The iteration—more specifically, one complete pass of the training dataset through the algorithm—is called epoch. you can set the number of epochs as a hyperparameter in training.

This is how a neural network learns. It learns from the signal sent by the cost function, similar to a human learning lessons from the past. It continues adjusting the weights (like a human) to constantly improve behaviors. It iterates the learning until it reaches the best result, like a human who wants to eventually become a better-self.

<figure><img src="../../.gitbook/assets/image (40) (1).png" alt=""><figcaption></figcaption></figure>

For the illustration purpose, you use a simple example with two input neurons (nodes), one hidden neuron, and one output neuron. In practice, you might have many neurons in each layer. Regardless of the number of neurons in the input, the hidden, and the output layer, the fundamental process of how a neural network learns remains the same.

### Code

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

In modern architecture it reduced down.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

## Resources

\[An Introduction to Neural Networks]\([https://victorzhou.com/blog/intro-to-neural-networks/](https://victorzhou.com/blog/intro-to-neural-networks/))

\[Introduction to Neural Networks | Stanford CS229]\([https://www.youtube.com/watch?v=MfIjxPh6Pys](https://www.youtube.com/watch?v=MfIjxPh6Pys))

\[Neural Networks: Zero to Hero - Andrej Karpathy]\([https://www.youtube.com/watch?v=VMj-3S1tku0\&list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ](https://www.youtube.com/watch?v=VMj-3S1tku0\&list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ))
