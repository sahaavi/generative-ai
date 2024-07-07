# Function Calling

Function calling lets developers create a description of a function in their code, then pass that description to a language model in a request. The response from the model includes the name of a function that matches the description and the arguments to call it with.

When working with a generative text model, it can be difficult to coerce the LLM to give consistent responses in a structured format such as JSON. Function calling makes it easy to work with LLMs via prompts and unstructured inputs, and have the LLM return a structured response that can be used to call an external function.

You can think of function calling as a way to get structured output from user prompts and function definitions, use that structured output to make an API request to an external system, then return the function response to the LLM to generate a response to the user. In other words, function calling extracts structured parameters from unstructured text or messages from users.&#x20;

In this example, you'll use function calling along with the chat modality in the Gemini model to help customers get information about products in the Google Store.

{% @github-files/github-code-block url="https://github.com/sahaavi/generative-ai/blob/main/gemini/intro_function_calling.ipynb" %}
