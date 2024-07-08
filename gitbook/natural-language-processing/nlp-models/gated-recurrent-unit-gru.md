# Gated Recurrent Unit (GRU)

It simplifies LSTM and is becoming increasingly popular in solving NLP problems. Compared to an LSTM, a GRU merges the pipeline C (cell state) and H (hidden state) into one. It’s like combining the short-term memory and the long-term memory into one memory.

<figure><img src="../../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

A GRU has two major gates: The reset gate: it determines how much information from the past should be carried on to the future. The update gate: it combines the forget and input gates in an LSTM into a single “update gate.” …It decides how much information should be forgotten. and how much information should be remembered. It then updates the information to the output as the memory passes to the next time step.

<figure><img src="../../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
