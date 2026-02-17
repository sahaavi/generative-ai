# Vector Search

You wanna find a product, but you only have a vague idea of what it looks like, and don't know the name or brand. Or you remember a lyric from a song, but you wanna know the name of the song and the artist as well as similar songs. Or you look for a vacation recommendation based on a few conditions like location, budget and time.

For enterprises, do you wanna develop visual search, natural language search and recommenders to both manage knowledge internally and improve the customer and partner experience externally? For example, externally, you could help customers find similar products through images, search for products through conversations and recommend products. Internally, you could help knowledge workers search for relevant documentation, find subject matter experts, SMEs and discover use cases across teams.

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Vector Search, a technology that focuses on semantic similarity can be used to perform all of these tasks. It has the ability to search through billions of semantically similar or related items.

Why is Vector Search important?

Let's look at how it differs from the traditional search technologies like keyword search. Keyword search follows a process that begins with crawling the web, indexing keywords and then serving the results by retrieval and ranking. The data is stored in tables and the search is only effective to a certain extent. As people increasingly demand more sophisticated search capabilities, they expect search engines to be more intelligent and have a better understanding of their intent. They also want search engines to perform a wider range of tasks such as generating summaries and making recommendations. However, traditional search technology faces a few challenges. It can't understand the intention and context of a query. It does not support multimodal search. And it lacks domain specificity.

To address these challenges, Vector Search technology converts data into a special vector called embeddings, which contains semantic meaning. The benefits of Vector Search are: Semantic understanding: Vector Search can find results that are similar in meaning to a query even if they do not contain the exact same keywords. This is useful for natural language queries where users may not be using precise or technical language. Multimodal search capabilities: Vector Search can be applied to various data types, including text, images and audio. This enables multimodal search applications where users can search for information using multiple types of data. Personalization and recommendation: Vector Search can be used to personalize search results and recommendations by leveraging its context understanding capability. This can help users find more relevant and interesting information.

In addition, Vector Search is a critical component in generative AI applications to help retrieve information fast and efficiently. It is becoming one of the most important components in AI and machine learning services.

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

Overall, Vector Search technology is transforming the way people engage with information. It allows for more relevant, efficient and personalized search experiences across a wide range of applications. As data volumes continue to grow and user expectations for search become more sophisticated, Vector Search is poised to play an increasingly crucial role in the future of search.

How does Vector Search work?

Step one, encode data into vectors by using AI models called, embedding models.

Step two, create an index to enable fast and scalable Vector Search.

Step three, search the vector space to find information that is similar to the query.

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

A slightly more detailed view from two perspectives. Build the Vector Search at development time. This involves generating embeddings, building and deploying an index. Query the vector space at serving time. This involves encoding a query, searching the vector space and serving results.

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

Encoding data is like generating a list of keywords from the book. Indexing is like creating an indexing system such as pairing each keyword with pages. Searching is like finding the keyword based on a search mechanism such as alphabetical order.

How we encode data [word-embeddings-encoding-text-to-meaningful-vectors](word-embeddings-encoding-text-to-meaningful-vectors/ "mention")

In Vector Search, the challenge is how to index the vector space to enable fast and efficient search. However, fast and scalable Vector Search isn't easy. It contains two major challenges, among others. How can you measure the distance between vectors, and how can you search vectors in a fast and scalable way?

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

How can you measure the distance between vectors? Imagine you have a multi-dimensional vector space where visual detection is impossible. How do you know that Paris and Tokyo are closer to each other than they are to Apple? When building vector search on Google Cloud, you can choose from four widely used metrics to measure the distance between vectors.

The selection depends on various factors, with the embedding model being one of the primary considerations. The first two metrics, Manhattan and Euclidean distance, measure the distance between the endpoints of the vectors. The third metric, cosine distance, measures the angle between two vectors and defines the vector similarity in terms of directions. The fourth metric, dot product distance, considers the similarity in terms of both the direction and the magnitude of two vectors.

<figure><img src="../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>

Cosine similarity is calculated by taking the cosine of the angle between the two vectors, where zero indicates that the vectors are completely aligned and one indicates that they are completely orthogonal.

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

Once you know how to measure the distance between two vectors, the next challenge is to efficiently find the similar vectors in the vast vector space.

Two search algorithms have seen extensive use: Brute-force, which is based on an accurate, exhaustive search approach, and TreeAh, which relies on an approximate tree search algorithm. TreeAh stands for shallow tree and Asymmetric Hashing. It is widely used in a production environment.

The brute-force algorithm typically consists of three steps. Step one, calculate the distances from the query to the other vectors in the vector space. Step two, sort all distances. Step three, find the top k nearest vectors. Because the size of the database can easily be in the millions or even billions, exhaustive search is impractical and the brute-force algorithm becomes a computational bottleneck.

The TreeAh algorithm accelerates search by using an approximate search technique called ANN, or approximate nearest neighbor. ANN enables fast and scalable search with billions of embeddings by dividing the search space into multiple spaces, indexing the spaces using a tree structure, and trading some accuracy for a significant speed-up over brute-force search.

<figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

In 2020, Google Research introduced ScaNN, which means Scalable Approximate Nearest Neighbor, a new ANN algorithm. ScaNN is the foundation for many Google services, including Google Search, YouTube, and its recommendation system. It is considered one of the best ANN algorithms in the industry, both in terms of accuracy and speed.

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

How does ScaNN enable fast and scalable Vector Search?

Consider the brute-force complexity, which is O(N\*d), where N is the number of vectors, and d is the number of dimensions.

To enhance Vector Search performance, you need to apply a combination of critical techniques, reduce the search space, also known as space pruning, and compress the vector size using data quantization. Also, you need to increase ranking efficiency by integrating business logics.

<figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>

To reduce the search space, ScaNN uses a multi-level tree search for space pruning. The first step is to divide the vector space into hierarchical partitions, as shown on the right. A search tree is then constructed to represent this structure, as shown on the left. Each node in the tree represents the centroid, the center point of a partition. Next, you select the partitions closest to the query. The red squares represent vector spaces that are close to the query, while the yellow squares indicate the spaces that are far from the query and will then be pruned.

<figure><img src="../.gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

You start by searching from the root node, the query, then moving to the branches, the partitions, and finally to the leaves, the sub-partitions. During this process, you prune the tree to eliminate irrelevant search space.

<figure><img src="../.gitbook/assets/image (89).png" alt=""><figcaption></figcaption></figure>

Last, you search for approximate data points within leaves, the most relevant sub-partitions.

<figure><img src="../.gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

The second technique is data quantization. Data quantization is used to compress data points to save space and reduce indexing time. For example, data quantization can be used to compress a nine-dimensional vector from nine floats to 12 bits.

<figure><img src="../.gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

The third technique is to incorporate business logic to retrieve only the data that is relevant. For example, you can use a filter to find resorts in the United States and dresses in the color red. From a technical perspective, this is known as restricting the search to a portion of the dataset.

<figure><img src="../.gitbook/assets/image (92).png" alt=""><figcaption></figcaption></figure>

ScaNN, Scalable Approximate Nearest Neighbor, is a combination of these techniques. Vertex AI Vector Search is built on a similar, more advanced version of ScaNN. Vertex AI Vector Search provides a fully managed similarity Vector Search service. It was launched in 2021 under the name Matching Engine. Powered by ScaNN and Vertex AI, the unified AI development platform, Vector Search is 30 to 50% less expensive than comparable services, while maintaining fast searching, lower latencies, and scaling to billions of vectors.

## Vector Search in Action

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Assume you are a data scientist and would like to improve the customer searching experience and help them find similar items. First, you get embeddings for each item, next, build an index on vector search with the embeddings and last, you can run a query on Vector Search to find similar items by their names. Let's explore how this works.&#x20;

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

The BigQuery table for items such as pants and socks is shown here. BigQuery is the primary data warehouse product on Google Cloud.&#x20;

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

You can easily get text embeddings in BigQuery by using the ML.EMBED\_TEXT function. Although the process is straightforward, the results are cutting edge. The large language model powered text embeddings are carefully organized in the embedding space with human level intelligence and common sense.&#x20;

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

You then export the embeddings to a JSON file and store them on Cloud Storage. Each embedding has 768 dimensions. Note that the number of dimensions is a hyper parameter that you can specify when you call the embedding API.&#x20;

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Afterward create an index by invoking the Vector Search APIs, you can designate the search algorithm, which is TreeAh in the demo, establish the Cloud Storage address of the JSON file and include parameters like the dimensions, number of items to retrieve and similarity measurement type. Google provides a rapid indexing service, which only takes a few minutes to index three digit megabytes.&#x20;

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

The final step is to deploy the index to an endpoint. The endpoint receives query requests from the front end and executes the Vector Search. The Vector Search engine is now ready to serve.&#x20;

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

To begin, provide the embedding of an item to the search engine. In a matter of milliseconds, you will receive a list of similar items. Please note that this is not a keyword search, but a semantic search. This means that the search engine understands the meaning of the search item and finds the closest information. This can provide a much better user experience for exploring and finding relevant items. Vector Search is also very easy to use. You can do it with just a few clicks or simple codings.

<figure><img src="../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

## Vector Search with RAG

<figure><img src="../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

Vector Search can be used to feed the LLM with relevant context in real time. The architecture to accomplish this process is called RAG, which stands for Retrieval Augmented Generation. To do this, you take the input prompt, query the real-time information using Vector Search, retrieve the top results, and append them to the original prompt. You then pass this augmented prompt with real-time context information to the LLM. Now, the LLM has not only the original user query, but also additional information that it can use to answer the query.

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

The RAG system can engage in conversations like this one using knowledge gained through Vector Search to respond to questions.

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>

## Resources

\[Vertex AI Embeddings for Text: Grounding LLMs made easy]\([https://cloud.google.com/blog/products/ai-machine-learning/how-to-use-grounding-for-your-llms-with-text-embeddings](https://cloud.google.com/blog/products/ai-machine-learning/how-to-use-grounding-for-your-llms-with-text-embeddings))
