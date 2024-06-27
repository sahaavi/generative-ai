# NLP Architecture on GCP

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

**Three Layers of NLP Architecture:**

1. **AI Foundation (Bottom Layer):**
   * **Google Cloud Infrastructure:**
     * **Networking and Security:** The foundation for all infrastructure and applications.
     * **Compute and Storage:** Decoupled to scale independently.
       * **Compute Advances:**
         * **Tensor Processing Unit (TPU):** Custom-developed ASICs for accelerating machine learning workloads, introduced in 2016. TPUs offer higher efficiency for specific tasks like matrix multiplication.
   * **Data Engineering Tools:**
     * **Dataflow:** Ingest and process batch and real-time data.
     * **BigQuery:** Analyze and uncover insights from data.
     * Both tools eliminate the need to manage and scale infrastructure manually.
2. **NLP Development Platform (Middle Layer):**
   * **Development Options:**
     * **Pre-built APIs:** Dialogflow API and Natural Language API.
     * **AutoML:** Customizable machine learning models.
     * **Vertex AI:** Custom training with Workbench.
3. **NLP Solutions (Top Layer):**
   * **Horizontal Solutions:** Applicable across industries.
     * **Examples:**
       * **Document AI (Doc AI)**
       * **Contact Center AI (CCAI)**
   * **Vertical Solutions:** Industry-specific applications.
     * **Examples:**
       * **Lending DocAI:** Automates mortgage document processing.
       * **Retail Search:** Enhances search and recommendation capabilities for retailers' digital properties.

This structured approach ensures scalability, efficiency, and targeted solutions for various NLP applications on Google Cloud.
