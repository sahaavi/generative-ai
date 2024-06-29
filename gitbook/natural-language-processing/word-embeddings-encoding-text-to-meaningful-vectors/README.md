# Word Embeddings: Encoding Text to Meaningful Vectors

**Intuition:**

* **Describing a Dog:** You might use dimensions like breed, age, size, color, owner, and friendliness.
* **Describing a Person:** You could mention IDs (e.g., driver’s license), physical stats (e.g., gender, height, weight), relationships (e.g., family, friends), social status (e.g., followers), hobbies, and even their pet.
* **Describing a Word:** For instance, "queen" could be described by its nature, origin, and associations like excitement and trust using quantitative dimensions.

**Concept:**

* **Vector Space Representation:**
  *

      <figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
  * **Words as Vectors:** Represent a word in a vector space with dimensions describing its properties.
  * **Distance and Similarity:** Similar words (e.g., queen and king) are close, while dissimilar words (e.g., queen and apple) are far apart.
  * **Analogies:** Capture relationships, e.g., King - Man + Woman = Queen.

**Word Embeddings:**

* **Definition:** A technique to encode text into meaningful, low-dimensional, dense vectors.
* **Advantages:**
  * **Low Dimensionality:** Vectors typically range from single-digit dimensions (small datasets) to four-digit dimensions (large datasets), unlike the high-dimensional vectors in one-hot encoding.
  * **Dense Vectors:** Each vector element usually contains a value, avoiding the sparsity problem.
  * **Capturing Relationships:** Similar words have similar vector representations.
* **Distributed Representation:** Indicates that the meaning of a word is spread across dimensions.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

**Training Embeddings:**

* **Neural Networks:** Instead of manually specifying values, a neural network learns the vector representations.
* **Magic of Word Embeddings:** They convert words into vectors that convey semantic similarities.

**Popular Algorithms/Models:**

* **Word2Vec:** Developed by Google.
* **GloVe:** Developed by Stanford.
* **FastText:** Developed by Facebook.
