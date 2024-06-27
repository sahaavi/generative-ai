# NLP with AutoML on GCP

* **Purpose:** AutoML, short for automated machine learning, aims to automate ML workflows to save time and effort in training and deploying ML models.
* **Context:** Training and deploying ML models can be time-consuming due to the need for repetitive tasks such as adding new data, trying different models, and tuning parameters.

**Key Technologies Behind AutoML:**

1. **Transfer Learning:**
   * **Concept:** Builds a knowledge base using pre-trained models, similar to gathering a library of books.
   * **Benefits:** Achieves high accuracy with smaller datasets and less computational power by leveraging models pre-trained on similar, larger datasets. This reduces the need for models to learn from scratch.
2. **Vertex AI Neural Architecture Search:**
   * **Concept:** Compares multiple models to find the optimal one, akin to searching for the best book in a library.
   * **Benefits:** Automatically finds and trains the best model by evaluating different models and hyperparameters.

**Functionality and Benefits:**

* **No-Code Solution:** Allows users to train high-quality custom machine learning models with minimal effort and little ML expertise.
* **Focus Areas:** Enables data scientists to concentrate on tasks like defining business problems in NLP or evaluating and improving model results.
* **Prototyping Tool:** Useful for quickly prototyping models and exploring new features of a dataset before investing in full-scale development.

**AutoML for NLP:**

* **Supported Data Types:** AutoML supports image, tabular, text, and video data. Text data is primarily used for NLP problems.
* **Objectives for Text Data:**
  1. **Text Classification:**
     * **Function:** Analyzes text data and returns a list of applicable categories.
     * **Example:** Classifies customer questions and comments into different categories for redirection to appropriate departments.
  2. **Entity Extraction:**
     * **Function:** Inspects text data for known entities and labels them.
     * **Example:** Labels social media posts with predefined entities such as time, location, and topic, aiding online search (similar to hashtags but created by machine).
  3. **Sentiment Analysis:**
     * **Function:** Inspects text data to identify the emotional opinion (positive, negative, or neutral).
     * **Example:** Determines the sentiment of customer feedback or social media comments.

**Combining Multiple Data Types and Objectives:**

* **Real-World Application:** Often requires combining various data types and objectives to solve a business problem.
  * **Example:** For a translation job, you might need to upload image or video data, convert it to text, and then translate the text into different languages.
