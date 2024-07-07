---
description: >-
  Vertex AI's TextGenerationModel and ChatModel have been used here for code
  purposes, but the concept is the same across all large language models.
---

# Prompt Design - Best Practices

### Prompt engineering best practices <a href="#prompt-engineering-best-practices" id="prompt-engineering-best-practices"></a>

Prompt engineering is all about how to design your prompts so that the response is what you were indeed hoping to see.

The idea of using "unfancy" prompts is to minimize the noise in your prompt to reduce the possibility of the LLM misinterpreting the intent of the prompt. Below are a few guidelines on how to engineer "unfancy" prompts.

In this section, you'll cover the following best practices when engineering prompts:

* Be concise
* Be specific, and well-defined
* Ask one task at a time
* Improve response quality by including examples
* Turn generative tasks to classification tasks to improve safety

#### Be concise <a href="#be-concise" id="be-concise"></a>

🛑 Not recommended. The prompt below is unnecessarily verbose.

```python
prompt = "What do you think could be a good name for a flower shop that specializes in selling bouquets of dried flowers more than fresh flowers? Thank you!"
```

✅ Recommended. The prompt below is to the point and concise.

```python
prompt = "Suggest a name for a flower shop that sells bouquets of dried flowers"
```

#### Be specific, and well-defined <a href="#be-specific-and-well-defined" id="be-specific-and-well-defined"></a>

Suppose that you want to brainstorm creative ways to describe Earth.

🛑 Not recommended. The prompt below is too generic.

```python
prompt = "Tell me about Earth"
```

✅ Recommended. The prompt below is specific and well-defined.

```python
prompt = "Generate a list of ways that makes Earth unique compared to other planets"
```

#### Ask one task at a time <a href="#ask-one-task-at-a-time" id="ask-one-task-at-a-time"></a>

🛑 Not recommended. The prompt below has two parts to the question that could be asked separately.

```python
prompt = "What's the best method of boiling water and why is the sky blue?"
```

✅ Recommended. The prompts below asks one task a time.

```python
prompt1 = "What's the best method of boiling water?"
prompt2 = "Why is the sky blue?"
```

### Watch out for hallucinations <a href="#watch-out-for-hallucinations" id="watch-out-for-hallucinations"></a>

Although LLMs have been trained on a large amount of data, they can generate text containing statements not grounded in truth or reality; these responses from the LLM are often referred to as "hallucinations" due to their limited memorization capabilities. Note that simply prompting the LLM to provide a citation isn’t a fix to this problem, as there are instances of LLMs providing false or inaccurate citations. Dealing with hallucinations is a fundamental challenge of LLMs and an ongoing research area, so it is important to be cognizant that LLMs may seem to give you confident, correct-sounding statements that are in fact incorrect.

Note that if you intend to use LLMs for the creative use cases, hallucinating could actually be quite useful.

Try the prompt like the one below repeatedly. You may notice that sometimes it will confidently, but inaccurately, say "The first elephant to visit the moon was Luna".

```python
prompt = "Who was the first elephant to visit the moon?"
```

Clearly the chatbot is hallucinating since no elephant has ever flown to the moon. But how do we prevent these kinds of inappropriate questions and more specifically, reduce hallucinations?

There is one possible method called the Determine Appropriate Response (DARE) prompt, which cleverly uses the LLM itself to decide whether it should answer a question based on what its mission is.

Let's see how it works by creating a chatbot for a travel website with a slight twist.

```python
chat_model = ChatModel.from_pretrained("chat-bison@002")

chat = chat_model.start_chat()
dare_prompt = """Remember that before you answer a question, you must check to see if it complies with your mission.
If not, you can say, Sorry I can't answer that question."""

print(
    chat.send_message(
        f"""
Hello! You are an AI chatbot for a travel web site.
Your mission is to provide helpful queries for travelers.

{dare_prompt}
"""
    )
)
```

Suppose we ask a simple question about one of Italy's most famous tourist spots.

```python
prompt = "What is the best place for sightseeing in Milan, Italy?"
```

Now let us pretend to be a not-so-nice user and ask the chatbot a question that is unrelated to travel.

```python
prompt = "Who was the first elephant to visit the moon?"
```

You can see that the DARE prompt added a layer of guard rails that prevented the chatbot from veering off course.

### Turn generative tasks into classification tasks to reduce output variability <a href="#turn-generative-tasks-into-classification-tasks-to-reduce-output-variability" id="turn-generative-tasks-into-classification-tasks-to-reduce-output-variability"></a>

#### **Generative tasks lead to higher output variability**

The prompt below results in an open-ended response, useful for brainstorming, but response is highly variable.

```python
prompt = "I'm a high school student. Recommend me a programming activity to improve my skills."
```

#### **Classification tasks reduces output variability**

The prompt below results in a choice and may be useful if you want the output to be easier to control.

```python
prompt = """I'm a high school student. Which of these activities do you suggest and why:
a) learn Python
b) learn JavaScript
c) learn Fortran
"""

print(generation_model.predict(prompt=prompt, max_output_tokens=256).text)
```

### Improve response quality by including examples <a href="#improve-response-quality-by-including-examples" id="improve-response-quality-by-including-examples"></a>

Another way to improve response quality is to add examples in your prompt. The LLM learns in-context from the examples on how to respond. Typically, one to five examples (shots) are enough to improve the quality of responses. Including too many examples can cause the model to over-fit the data and reduce the quality of responses.

Similar to classical model training, the quality and distribution of the examples is very important. Pick examples that are representative of the scenarios that you need the model to learn, and keep the distribution of the examples (e.g. number of examples per class in the case of classification) aligned with your actual distribution.

#### **Zero-shot prompt**

Below is an example of zero-shot prompting, where you don't provide any examples to the LLM within the prompt itself.

```python
prompt = """Decide whether a Tweet's sentiment is positive, neutral, or negative.

Tweet: I loved the new YouTube video you made!
Sentiment:
"""

print(generation_model.predict(prompt=prompt, max_output_tokens=256).text)
```

#### **One-shot prompt**

Below is an example of one-shot prompting, where you provide one example to the LLM within the prompt to give some guidance on what type of response you want.

```python
prompt = """Decide whether a Tweet's sentiment is positive, neutral, or negative.

Tweet: I loved the new YouTube video you made!
Sentiment: positive

Tweet: That was awful. Super boring 😠
Sentiment:
"""

print(generation_model.predict(prompt=prompt, max_output_tokens=256).text)
```

#### **Few-shot prompt**

Below is an example of few-shot prompting, where you provide a few examples to the LLM within the prompt to give some guidance on what type of response you want.

```python
prompt = """Decide whether a Tweet's sentiment is positive, neutral, or negative.

Tweet: I loved the new YouTube video you made!
Sentiment: positive

Tweet: That was awful. Super boring 😠
Sentiment: negative

Tweet: Something surprised me about this video - it was actually original. It was not the same old recycled stuff that I always see. Watch it - you will not regret it.
Sentiment:
"""

print(generation_model.predict(prompt=prompt, max_output_tokens=256).text)
```

#### **Choosing between zero-shot, one-shot, few-shot prompting methods**

Which prompt technique to use will solely depends on your goal. The zero-shot prompts are more open-ended and can give you creative answers, while one-shot and few-shot prompts teach the model how to behave so you can get more predictable answers that are consistent with the examples provided.

* Language models perform well with formatted text; using structured text like pseudocode can improve results
* Decompose tasks into smaller pieces in your prompt to make the language model generate each piece; automate decomposition for better performance
* Elicit reasoning capabilities from the model by carefully tuning the prompt, such as using "Let's think step-by-step"
* Ensemble results of multiple models for more accurate answers and use randomness for greater heterogeneity in responses
* Combine prompting techniques (e.g., few-shot, Chain of Thought, ensembling) to increase performance, but be mindful of the impact on latency and compute costs
