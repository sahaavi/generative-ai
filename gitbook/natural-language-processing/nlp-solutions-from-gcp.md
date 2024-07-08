# NLP Solutions from GCP

### Contact Center Artificial Intelligence (CCAI)

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

* **Purpose:** Enhance operational efficiency in contact centers using AI with minimal AI expertise required.
* **Integration:** Seamlessly integrates with existing company infrastructure.

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Key Features:**

1. **Speech Recognition:**
   * Converts customer speech to text using Automatic Speech Recognition (ASR), also known as Speech-to-Text (SST).
2. **Natural Language Understanding (NLU):**
   * Interprets and understands the customer’s spoken words to determine their intent.
3. **Text-to-Speech (TTS):**
   * Converts text responses back into speech, creating an audio stream or file for playback to the customer.
4. **Voice Personalization:**
   * Generates different voices for audio streams, allowing customization by brand or regional accents.
5. **Seamless Integration:**
   * Provides one-click integration with leading telephony providers like AT\&T for a smooth customer service experience.

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Components of Contact Center AI:**

1. **Dialogflow:**
   * **Function:** Creates virtual agents that interact with customers.
   * **Technology:** Utilizes NLU to understand and respond to customer queries.
   * **Support:** Powers Agent Assist.
2. **Agent Assist:**
   * **Function:** Supports human agents by monitoring conversations and offering suggestions based on customer needs and knowledge databases.
   * **Capability:** Enhances the efficiency and accuracy of human agents during customer interactions.
3. **Insights:**
   * **Function:** Analyzes historical conversations to identify trends, successes, and areas needing improvement.
   * **Role:** Acts as a data analyst for conversation analytics, aiding Contact Center management in decision-making.

**Benefits:**

* **Efficiency:** Streamlines operations by automating interactions and assisting human agents.
* **Personalization:** Customizes interactions to align with brand identity and regional customer preferences.
* **Integration:** Easily connects with existing telephony systems for enhanced service delivery.

### Document AI

* **Purpose:** Document AI is a document understanding solution that converts unstructured data, such as emails, images, documents, and PDFs, into structured data for easier analysis and consumption.
* **Example Use Case:** Reading a driver’s license, extracting fields like state and name, converting this information to a structured data form, and saving it in a JSON file for easy search, classification, and analytics.

**Key Technologies Behind Document AI:**

* **Natural Language Processing (NLP):** Enables understanding and processing of human language.
* **Computer Vision and Optical Character Recognition (OCR):** Facilitates the extraction of text from images.
* **Pre-trained Machine Learning Models:** Tailored for processing high-value, high-volume documents.

**Capabilities of Document AI:**

1. **Convert Images to Text:** Uses OCR to digitize text from images.
2. **Classify Documents:** Automatically categorizes different types of documents.
3. **Analyze and Extract Entities:** Identifies and extracts specific data points from documents.
4. **Produce New Insights:** Generates actionable insights from structured data.

**Document AI Workflow:**

1. **Document Submission:** Documents are sent for processing.
   * **Output:** Returns one or more document objects with extracted, structured information.
   * **Reference:** For detailed instructions, see "Sending a processing request."
2. **Processor Selection or Creation:**
   * **Choosing a Processor:** Select an existing processor suitable for the use case.
   * **Creating a Processor:** Custom processors can be created using the Google Cloud Console.
3. **Human Review:** Evaluate the accuracy of the output, interpret results, and address any issues overlooked by the processor.
4. **Result Storage:** Save results in a database or data warehouse for further analysis.

**Processor Types and Selection:**

<figure><img src="../.gitbook/assets/image (7) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Summary of Processor Benefits:**

* **General Processor:** Versatile and cost-effective for general tasks.
* **Specialized Processor:** Superior performance for specific document types.
* **Custom Processor (Build-it-yourself):** Full control and IP ownership for unique problems.
* **Custom Processor (Built with Google):** Optimal quality and co-branding opportunities, leveraging combined expertise.
