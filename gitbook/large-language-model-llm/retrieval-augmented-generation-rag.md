# Retrieval Augmented Generation (RAG)

As the context window of llms getting larger it's getting more convenient to feed personal or company data to the llms in order to produce result based on those data. Because llm are trained on publicly available data and it has no idea of your personal data.&#x20;

<figure><img src="../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>

From the documents it needs to store data through indexing so that it can retrive through search based on questions.

<figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

## Indexing

### Document Loading

The aspect of indexing is -  we have some internal documents and we want load and put into Retriever. The goal of retriever is simply given an input question, I want to search through my documents that are relate to my question in some way.

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

As embeddings can not take infinite tokens, so that we have to split documents before embeddings

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

## Retrieving

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>
