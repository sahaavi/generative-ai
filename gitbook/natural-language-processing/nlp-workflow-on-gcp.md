# NLP workflow on GCP

* **Purpose:** Vertex AI, Google’s AI Platform, provides developers and data scientists with a unified environment to build custom ML models.
* **Analogy:** The process of building an NLP model using Vertex AI is akin to serving food in a restaurant, involving preparation, experimentation, and serving.

**Three Main Stages:**

1. **Data Preparation:**
   * **Analogy:** Similar to preparing raw ingredients in a restaurant.
   * **Uploading Data:** Comparable to gathering raw ingredients in the kitchen. Data can come from Cloud Storage or a local machine and can be labeled or unlabeled.
     * **Labeled Data:** If the goal is sentiment analysis, sample sentences must be tagged as positive or negative. Labels can be added manually or via Google’s paid label service through the Vertex console.
     * **Unlabeled Data:** For clustering analysis or latent semantic indexing (LSI), which identify patterns and co-occurrence of words.
   * **Feature Engineering:** Comparable to peeling, chopping, and rinsing vegetables. The data needs to be processed before training starts.
2. **Model Training:**
   * **Analogy:** Similar to experimenting with recipes.
   * **Steps:**
     * **Model Training:** Like cooking recipes, involves iterative training of the model.
     * **Model Evaluation:** Similar to tasting the dishes, involves evaluating the model to refine and improve it.
   * **Cycle:** Training and evaluation form a cycle, where the model is trained, evaluated, and retrained.
3. **Model Serving:**
   * **Analogy:** Similar to serving dishes on the table and monitoring restaurant performance.
   * **Steps:**
     * **Model Deployment:** Moving the model into production is like serving dishes to customers. Three deployment options:
       * **Endpoint Deployment:** For immediate results with low latency, such as real-time translation.
       * **Batch Prediction:** For processing accumulated data with a single request, like sending ads based on user behavior.
       * **Offline Prediction:** For deploying models outside the cloud in specific environments.
     * **Model Monitoring:** Similar to monitoring restaurant workflow and performance, involves tracking the model's performance and addressing issues like data drifting.

**Iterative Nature of the Workflow:**

* **Non-linear Process:** The NLP workflow is iterative, not linear.
  * **Revisiting Data:** During model training, you might need to revisit and refine raw data.
  * **Adjustments:** During model monitoring, if data drifting occurs (accuracy drops), data sources and model parameters may need adjustment.
* **MLOps:** These steps can be automated using machine learning operations (MLOps), streamlining the entire process.
