# Natural Language Processing

**Definition:** NLP teaches computers to understand human languages, a task that initially seems impossible due to the complexity and nuance of language. However, with nearly unlimited memory (e.g., cloud storage), supercomputing power (e.g., TPU), and advanced ML techniques, computers can achieve this.

**NLP as an Input-Process-Output System:**

<figure><img src=".gitbook/assets/image (8) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Input:** Natural human languages (text or speech).
* **Process:**
  1. **Text Representation:** Translating human language to machine language.
  2. **Language Processing:**
     * **Rule-based Reasoning:** Using hand-coded rules like dictionary lookups. Example: Matching "hello" in English to "hola" in Spanish.
     * **Machine Learning:** The computer learns rules from large datasets. Example: Predicting ratings based on customer feedback. This method is much more scalable. Detailed explanations of NLP models will be covered in Modules 4 and 5.
* **Output:**
  * **Text Classification:** Predicting labels for documents.
    * Examples:
      * **Sentiment Analysis:** Deciding the rating based on customer comments.
      * **Spam Identification:** Determining if an email is spam.
      * **Topic Classification:** Identifying the topic of content.
  * **Entity Extraction (Entity Recognition):** Identifying specific entities within text.
    * Example: Google Assistant recognizing weather (topic), today (date), and Denver (location) from a query.
  * **Machine Translation:** Translating text from one language to another.
  * **Interactive Conversation:** Implementing chatbots for real-time interaction.

<figure><img src=".gitbook/assets/image (9) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

You may already discover that NLP is a marriage between linguistics and artificial intelligence. It’s multidisciplinary, and involves linguistics, computer science, AI and ML, and statistics.

Natural language is a sequence. The order of the words matters. For example, look at the sentence “A dog is chasing a person.” If you change the order, the sentence might completely change the meaning, like “A person is chasing a dog,” or no longer make sense like “Dog is a person a chasing.” Therefore, sequence models have been used to capture and model natural language.&#x20;

Sequences can be the input and the output of a machine learning model.

<figure><img src=".gitbook/assets/image (10) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Broadly, sequence models fit into three types: one-to-sequence, sequence-to-one, and sequence-to-sequence. In a one-to-sequence model, one input is passed in, and the model generates a sequence as the output. A typical example is image captioning, where the description of an image, normally a few sentences, is generated based on this one image. In a sequence-to-one model, a sequence is passed in and one output is generated. For example, sentiment analysis is a typical sequence-to-one problem. Based on the comments of a few sentences, the machine can generate one rating. Finally, in a sequence-to-sequence model, sequences serve as both the input to and the output of the model. Google Translate is a typical example in dealing with sequence-to-sequence problems.

<figure><img src=".gitbook/assets/image (21) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Challenge:** A computer only understands digits, so feeding text into an NLP model requires converting it into a numeric format while retaining its meaning.

**Comparison with Other Data Types:**

1. **Tabular Data:**
   * **Ease of Use:** Most tabular data is already numeric, and non-numeric columns can be easily converted into numeric values.
2. **Image Data:**
   * **Conversion Method:** Images can be converted into numbers using pixels.
   * **Explanation:** Each cell in the matrix of pixels represents the intensity of the corresponding pixel in the image.
3. **Audio Data:**
   * **Conversion Method:** Audio can be converted into numbers using waves.
   * **Explanation:** Sample the wave and record its amplitude at fixed-time intervals, representing the audio as an array of amplitudes.
4. **Text Data:**
   * **Challenge:** Converting text into numbers is less obvious than with other data types.

**Steps for Text Representation in NLP:**

1. **Tokenization:**
   * **Purpose:** Divide the text into smaller language units, such as words or subwords.
   * **Explanation:** This is how a computer reads text, breaking it down into manageable parts.
2. **Preprocessing:**
   * **Purpose:** Clean and normalize the text data.
   * **Examples:**
     * **Stemming/Lemmatization:** Reducing words to their root forms.
     * **Punctuation Removal:** Eliminating punctuation to focus on the core text.
3. **Text Representation:**
   * **Purpose:** Convert the preprocessed language units into numbers that represent some meanings.
   * **Explanation:** This step allows a computer to understand the text, not just read it.
   * **Output:** The result is typically vectors that can be fed into ML models to solve specific tasks.

**Deep Dive into Text Representation:**

* **NLP Libraries:** Tools like TensorFlow simplify these steps by providing functions that hide the underlying complexities.
* **Manual Implementation:** Understanding these steps is crucial if you want to build your own NLP applications from scratch.
