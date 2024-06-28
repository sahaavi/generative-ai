# Transfer Learning

* **Expensive Computation:** Training word embeddings like Word2Vec from scratch can be computationally intensive and time-consuming.
* **Pre-trained Embeddings:** A practical approach is to use pre-trained embeddings, which are trained on large datasets and then fine-tuned for specific tasks.

**TensorFlow Hub (TF-Hub):**

* **Purpose:** A library for sharing and reusing machine learning model components, including pre-trained embeddings.
* **Modules:** Self-contained pieces of TensorFlow graphs, including weights and assets. These modules can be easily integrated into your models.

Using TensorFlow Hub:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

* **Installation and Import:**
  * Install the `tensorflow-hub` library.
  * Import the necessary Keras layers.
* **Loading a Pre-trained Embedding:**
  * **Example:** NNLM (Neural Probabilistic Language Model) with 50 dimensions, available as `nnlm-en-dim50` on TF-Hub.
  * **URL:** The module can be accessed via its URL, for instance, `https://tfhub.dev/google/nnlm-en-dim50/2`.
* **Integrating with Keras:**
  * **Layer Initialization:** Pass the module URL to the TensorFlow Hub constructor.
  * **Model Integration:** Use the module as a Keras layer in your model.
  * **Dimension Specification:** You can specify the number of dimensions for the embeddings, such as 50 in this example.

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

**Configuration:**

* **Trainable Embeddings:**
  * **Dataset Size Consideration:**
    * **Large Dataset:** Set `trainable=True` to fine-tune the embeddings and avoid overfitting.
    * **Small Dataset:** Set `trainable=False` to freeze the embeddings and prevent overfitting.
