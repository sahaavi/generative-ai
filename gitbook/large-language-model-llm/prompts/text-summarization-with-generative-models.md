# Text Summarization with Generative Models

### Overview <a href="#overview" id="overview"></a>

Text summarization produces a concise and fluent summary of a longer text document. There are two main text summarization types: extractive and abstractive. Extractive summarization involves selecting critical sentences from the original text and combining them to form a summary. Abstractive summarization involves generating new sentences representing the original text's main points. In this notebook, you go through a few examples of how large language models can help with generating summaries based on text.

Learn more about text summarization in the [official documentation](https://cloud.google.com/vertex-ai/docs/generative-ai/text/summarization-prompts).

#### Objective <a href="#objective" id="objective"></a>

In this tutorial, you will learn how to use generative models to summarize information from text by working through the following examples:

* Transcript summarization
* Summarizing text into bullet points
* Dialogue summarization with to-dos
* Hashtag tokenization
* Title & heading generation

You also learn how to evaluate model-generated summaries by comparing to human-created summaries using ROUGE as an evaluation framework.

### Text Summarization <a href="#text-summarization" id="text-summarization"></a>

#### Transcript summarization <a href="#transcript-summarization" id="transcript-summarization"></a>

In this first example, you summarize a piece of text on quantum computing.

```python
prompt = """
Provide a very short summary, no more than three sentences, for the following article:

Our quantum computers work by manipulating qubits in an orchestrated fashion that we call quantum algorithms.
The challenge is that qubits are so sensitive that even stray light can cause calculation errors — and the problem worsens as quantum computers grow.
This has significant consequences, since the best quantum algorithms that we know for running useful applications require the error rates of our qubits to be far lower than we have today.
To bridge this gap, we will need quantum error correction.
Quantum error correction protects information by encoding it across multiple physical qubits to form a “logical qubit,” and is believed to be the only way to produce a large-scale quantum computer with error rates low enough for useful calculations.
Instead of computing on the individual qubits themselves, we will then compute on logical qubits. By encoding larger numbers of physical qubits on our quantum processor into one logical qubit, we hope to reduce the error rates to enable useful quantum algorithms.

Summary:

"""

print(
    generation_model.predict(
        prompt, temperature=0.2, max_output_tokens=1024, top_k=40, top_p=0.8
    ).text
)
```

Instead of a summary, we can ask for a TL;DR ("too long; didn't read"). You can compare the differences between the outputs generated.

```python
prompt = """
Provide a TL;DR for the following article:

Our quantum computers work by manipulating qubits in an orchestrated fashion that we call quantum algorithms. 
The challenge is that qubits are so sensitive that even stray light can cause calculation errors — and the problem worsens as quantum computers grow. 
This has significant consequences, since the best quantum algorithms that we know for running useful applications require the error rates of our qubits to be far lower than we have today. 
To bridge this gap, we will need quantum error correction. 
Quantum error correction protects information by encoding it across multiple physical qubits to form a “logical qubit,” and is believed to be the only way to produce a large-scale quantum computer with error rates low enough for useful calculations. 
Instead of computing on the individual qubits themselves, we will then compute on logical qubits. By encoding larger numbers of physical qubits on our quantum processor into one logical qubit, we hope to reduce the error rates to enable useful quantum algorithms.

TL;DR:
"""

print(
    generation_model.predict(
        prompt, temperature=0.2, max_output_tokens=1024, top_k=40, top_p=0.8
    ).text
)
```

#### Summarize text into bullet points <a href="#summarize-text-into-bullet-points" id="summarize-text-into-bullet-points"></a>

In the following example, you use same text on quantum computing, but ask the model to summarize it in bullet-point form. Feel free to change the prompt.

```python
prompt = """
Provide a very short summary in four bullet points for the following article:

Our quantum computers work by manipulating qubits in an orchestrated fashion that we call quantum algorithms.
The challenge is that qubits are so sensitive that even stray light can cause calculation errors — and the problem worsens as quantum computers grow.
This has significant consequences, since the best quantum algorithms that we know for running useful applications require the error rates of our qubits to be far lower than we have today.
To bridge this gap, we will need quantum error correction.
Quantum error correction protects information by encoding it across multiple physical qubits to form a “logical qubit,” and is believed to be the only way to produce a large-scale quantum computer with error rates low enough for useful calculations.
Instead of computing on the individual qubits themselves, we will then compute on logical qubits. By encoding larger numbers of physical qubits on our quantum processor into one logical qubit, we hope to reduce the error rates to enable useful quantum algorithms.

Bullet points:

"""

print(
    generation_model.predict(
        prompt, temperature=0.2, max_output_tokens=256, top_k=1, top_p=0.8
    ).text
)
```

#### Dialogue summarization with to-dos <a href="#dialogue-summarization-with-to-dos" id="dialogue-summarization-with-to-dos"></a>

Dialogue summarization involves condensing a conversation into a shorter format so that you don't need to read the whole discussion but can leverage a summary. In this example, you ask the model to summarize an example conversation between an online retail customer and a support agent, and include to-dos at the end.

```python
prompt = """
Please generate a summary of the following conversation and at the end summarize the to-do's for the support Agent:

Customer: Hi, I'm Larry, and I received the wrong item.

Support Agent: Hi, Larry. How would you like to see this resolved?

Customer: That's alright. I want to return the item and get a refund, please.

Support Agent: Of course. I can process the refund for you now. Can I have your order number, please?

Customer: It's [ORDER NUMBER].

Support Agent: Thank you. I've processed the refund, and you will receive your money back within 14 days.

Customer: Thank you very much.

Support Agent: You're welcome, Larry. Have a good day!

Summary:
"""

print(
    generation_model.predict(
        prompt, temperature=0.2, max_output_tokens=256, top_k=40, top_p=0.8
    ).text
)
```

#### Hashtag tokenization <a href="#hashtag-tokenization" id="hashtag-tokenization"></a>

Hashtag tokenization is the process of taking a piece of text and getting the hashtag "tokens" out of it. You can use this, for example, if you want to generate hashtags for your social media campaigns. In this example, you take [this tweet from Google Cloud](https://twitter.com/googlecloud/status/1649127992348606469) and generate some hashtags you can use.

```python
prompt = """
Tokenize the hashtags of this tweet:

Google Cloud
@googlecloud
How can data help our changing planet? 🌎

In honor of #EarthDay this weekend, we’re proud to share how we’re partnering with
@ClimateEngine
 to harness the power of geospatial data and drive toward a more sustainable future.

Check out how → https://goo.gle/3mOUfts
"""

print(
    generation_model.predict(
        prompt, temperature=0.8, max_output_tokens=1024, top_k=40, top_p=0.8
    ).text
)
```

#### Title & heading generation <a href="#title-and-heading-generation" id="title-and-heading-generation"></a>

Below, you ask the model to generate five options for possible title/heading combos for a given piece of text.

```python
prompt = """
Write a title for this text, give me five options:
Whether helping physicians identify disease or finding photos of “hugs,” AI is behind a lot of the work we do at Google. And at our Arts & Culture Lab in Paris, we’ve been experimenting with how AI can be used for the benefit of culture.
Today, we’re sharing our latest experiments—prototypes that build on seven years of work in partnership the 1,500 cultural institutions around the world.
Each of these experimental applications runs AI algorithms in the background to let you unearth cultural connections hidden in archives—and even find artworks that match your home decor."
"""

print(
    generation_model.predict(
        prompt, temperature=0.8, max_output_tokens=256, top_k=1, top_p=0.8
    ).text
)
```

### Evaluation <a href="#evaluation" id="evaluation"></a>

You can evaluate the outputs from summarization tasks using [ROUGE](https://en.wikipedia.org/wiki/ROUGE\_\(metric)) as an evaluation framework. ROUGE (Recall-Oriented Understudy for Gisting Evaluation) are measures to automatically determine the quality of a summary by comparing it to other (ideal) summaries created by humans. The measures count the number of overlapping units such as n-gram, word sequences, and word pairs between the computer-generated summary to be evaluated and the ideal summaries created by humans.

The first step is to install the ROUGE library.

```python
!pip install rouge
```

Create a summary from a language model that you can use to compare against a human-generated summary.

```python
from rouge import Rouge

ROUGE = Rouge()

prompt = """
Provide a very short, maximum four sentences, summary for the following article:

Our quantum computers work by manipulating qubits in an orchestrated fashion that we call quantum algorithms.
The challenge is that qubits are so sensitive that even stray light can cause calculation errors — and the problem worsens as quantum computers grow.
This has significant consequences, since the best quantum algorithms that we know for running useful applications require the error rates of our qubits to be far lower than we have today.
To bridge this gap, we will need quantum error correction.
Quantum error correction protects information by encoding it across multiple physical qubits to form a “logical qubit,” and is believed to be the only way to produce a large-scale quantum computer with error rates low enough for useful calculations.
Instead of computing on the individual qubits themselves, we will then compute on logical qubits. By encoding larger numbers of physical qubits on our quantum processor into one logical qubit, we hope to reduce the error rates to enable useful quantum algorithms.

Summary:

"""

candidate = generation_model.predict(
    prompt, temperature=0.1, max_output_tokens=1024, top_k=40, top_p=0.9
).text

print(candidate)
```

You will also need a human-generated summary that we will use to compare to the `candidate` generated by the model. We will call this `reference`.

```python
reference = "Quantum computers are sensitive to noise and errors. To bridge this gap, we will need quantum error correction. Quantum error correction protects information by encoding across multiple physical qubits to form a “logical qubit”."
```

Now you can take the candidate and reference to evaluate the performance. In this case, ROUGE will give you:

* `rouge-1`, which measures unigram overlap
* `rouge-2`, which measures bigram overlap
* `rouge-l`, which measures the longest common subsequence

```python
ROUGE.get_scores(candidate, reference)
```
