# Bag of Words

**Challenge:** How to represent text in a numeric format while retaining its meaning.

<figure><img src="../.gitbook/assets/image (11) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Subproblems:**

1. Turn text into numbers that retain meaning (e.g., relationships between words such as similarity and difference).
2. Turn text into numbers that can be fed into an ML model (e.g., relatively dense matrices or vectors to avoid overfitting).

**Early Methods:**

1. **Morse Code and ASCII:**
   * **Morse Code:** Uses dots and dashes to represent characters.
   * **ASCII Code:** Uses numeric codes to represent characters.
   * **Limitations:** Neither conveys meaning beyond raw text. They work at the character level, leading to inefficient vectors for ML models.

Modern Text Representation Techniques:

<figure><img src="../.gitbook/assets/image (12) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**One-Hot Encoding:**

* **Process:**
  * Create a vector whose length equals the vocabulary size.
  * Place a “1” at the position corresponding to the word and “0”s elsewhere.
* **Example:**
  * Consider the sentence "A dog is chasing a person."
  *

      <figure><img src="../.gitbook/assets/image (20) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
  * To turn each word to a vector, you must first create a vector whose length equals the size of the vocabulary.
  * Assume you have a vocabulary that includes six words: Vocabulary: \["dog", "chase", "person", "my", "cat", "run"]
  *

      <figure><img src="../.gitbook/assets/image (13) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
  * By conducting one-hot encoding, you converted the sentence “A dog is chasing a person” into a matrix that an ML model takes.![](<../.gitbook/assets/image (21) (1) (1) (1).png>)
* **Advantages:**
  * Intuitive and easy to implement.
* **Disadvantage:**
  * No relationships between words. The vectors that represent each word are distinct from each other.
  * High-dimensional and sparse vectors, leading to potential overfitting.
  *   Most of the values of each vector are zeros, which means that this is a super sparse representation.

      <figure><img src="../.gitbook/assets/image (15) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Bag-of-Words:**

* **Process:**
  * Build a vocabulary from the text.
  * Create a vector indicating the frequency of each word.
* **Example:**
  *

      <figure><img src="../.gitbook/assets/image (22) (1) (1).png" alt=""><figcaption></figcaption></figure>
  *   Please note sometimes you might not care about the frequency, but only the occurrence of the words. You can simply use 1 and 0 to represent whether this word exists in the text.

      <figure><img src="../.gitbook/assets/image (23) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (16) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

If two sentences have similar vocabulary, they might have similar meanings and the two vectors that represent them are close in the vector space.

<figure><img src="../.gitbook/assets/image (17) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

For example, bag-of-words does not consider the order of the words and that is why it’s called a “bag” of words.

“A person is chasing a dog” and “A dog is chasing a person” would have the same representation in bag-of-words despite their opposite meanings.

<figure><img src="../.gitbook/assets/image (18) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

The basic vectorization methods such as one-hot encoding and bag-of-words are not ideal. &#x20;

Two major problems that have not been solved include: first, the high-dimensional and sparse vectors; and second, the lack of relationship between words.

<figure><img src="../.gitbook/assets/image (19) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
