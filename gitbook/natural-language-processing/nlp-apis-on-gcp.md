# NLP APIs on GCP

**Pre-built APIs: Dialogflow and Natural Language API**

**Dialogflow API:**

* **Purpose:** A natural language understanding (NLU) platform to integrate conversational interfaces into various applications (mobile apps, web applications, devices, bots, IVR systems).
* **Capabilities:**
  * Analyzes text and audio inputs.
  * Responds via text or synthetic speech.
* **Services:**

<div align="left">

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

</div>

**Key Concepts in Dialogflow:**

1. **Intent:** Represents the goal/topic of a conversation (e.g., setting a reminder, checking weather).
   * **Intent Matching:** Uses rule-based reasoning (decision trees) and machine learning models to identify intents.
2. **Entities:** Specific details related to an intent (e.g., dates, times, names).
   * **Types:** Predefined system entities (common data types) and custom entities (user-defined).
3. **Context:** Controls the flow of the conversation by maintaining context.
   * **Input Contexts:** Influence intent matching based on active contexts.
   * **Output Contexts:** Set active contexts for subsequent interactions.

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Natural Language API:**

* **Purpose:** Apply natural language understanding (NLU) using pre-trained models.
* **Key Features:**
  * **Sentiment Analysis:** Determine sentiment in text.
  * **Entity Analysis:** Identify entities within text.
  * **Entity Sentiment Analysis:** Determine sentiment toward entities.
  * **Content Classification:** Classify content into categories.
  * **Syntax Analysis:** Analyze the grammatical structure of text.

**Healthcare Natural Language API:**

* **Purpose:** Analyze insights from unstructured medical text.
* **Key Features:**
  * Extract machine-readable medical insights.
  * Build custom knowledge extraction models with AutoML Entity Extraction for Healthcare (no coding required).
