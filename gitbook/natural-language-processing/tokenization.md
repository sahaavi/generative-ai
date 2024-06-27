# Tokenization

**Introduction:**

* **Purpose:** Tokenization is the first step in preparing text for ML models. It divides text into smaller language units called tokens.
* **Example:** The sentence “a dog is chasing a person” is split into separate words.

**Challenges in Tokenization:**

1. **Language Differences:**
   * **English:** Tokenization is straightforward using whitespace as a delimiter.
   * **Chinese:** The sentence 一条狗在追一个人 (Chinese for “A dog is chasing a person”) lacks spaces between characters, making tokenization complex.
2. **Defining Tokens:**
   * **Question:** How do you define smaller language units?
   * **Answer:** Tokens can exist at different levels, such as characters, subwords, words, phrases, and sentences.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**Types of Tokens:**

1. **Character Tokens:**
   * **Example:** "dog" is split into "d-o-g".
2. **Subword Tokens:**
   * **Example:** "chasing" is split into "chase" and "ing".
3. **Word Tokens:**
   * **Example:** Text is split by whitespaces.
4. **Phrase Tokens:**
   * **Example:** Text is split by phrases, e.g., "a dog" and "is chasing".
5. **Sentence Tokens:**
   * **Example:** Text is split by punctuation.

**Choosing the Tokenization Type:**

* **Common Algorithm:** Word tokenization is widely used.
* **Factors:** The choice depends on the NLP libraries and models being used.

**Further Preparation: Preprocessing:**

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* **Lowercasing:** Convert all text to lowercase.
* **Stemming:** Reduce words to their root forms.
  * **Example:** "running", "ran", "runs" -> "run".
* **Stopword Removal:** Remove low-information words like “a” and “the”.
* **Normalization:** Transform text into a standard form.
  * **Example:** "lol" -> "laugh out loud", "tmr" -> "tomorrow".

**Using TensorFlow for Preprocessing:**

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* **TextVectorization API:**
  * **Function:** Maps text features to integer sequences, including preprocessing, tokenization, and vectorization.
  * **Benefit:** Allows all text preparation work to be done in one place.

**Using TensorFlow for Tokenization:**

* **Step-by-Step Guide:**
  1.  **Import Tokenizer API:**

      ```python
      from tensorflow.keras.preprocessing.text import Tokenizer
      ```
  2.  **Represent the Sentence:**

      ```python
      sentences = ["A dog is chasing a person"]
      ```
  3.  **Initialize the Tokenizer:**

      ```python
      tokenizer = Tokenizer(num_words=100)
      ```
  4.  **Fit the Tokenizer:**

      ```python
      tokenizer.fit_on_texts(sentences)
      ```
  5.  **Check the Tokens:**

      ```python
      word_index = tokenizer.word_index
      print(word_index)
      ```
* **Example Output:**
* `"a"` has a value of 1
* `"dog"` has a value of 2
*

    ```
    {'a': 1, 'dog': 2, 'is': 3, 'chasing': 4, 'person': 5}
    ```

#### Summary:

Tokenization is essential for preparing text data for machine learning models. It involves dividing text into tokens, which can be words, subwords, or other units. Different languages and applications may require different tokenization strategies. TensorFlow and other NLP libraries provide tools to facilitate tokenization and preprocessing, streamlining the process of converting text into a format suitable for ML models.
